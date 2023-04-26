---
layout: post
title:  "Rails activerecord after_create vs after_create_commit"
date:   2023-04-26 14:59:44 +0545
categories: Rails, Ruby
---
#### Background  
I was working on a chat application. Pusher was used as a real-time communication layer between the server and the client. Here the pusher event was triggered after creating a message. Which is simple and it works perfectly.

{% highlight ruby %}
after_create :notify_pusher
private
def notify_pusher
  pusher.trigger('my-channel', 'my-event', {
    message: 'hello world'
  })
end

{% endhighlight %}

This works only for text messages. I have noticed an issue when sending a photo message. While sending a photo message, sent message is appearing to the receiver chat box with empty attachment. After debugging I found something is wrong with the `after_create` ActiveRecord callback used. Since I was using ActiveStorage, I started to search if there is any callback in ActiveStorage which triggers after upload attachment. Unfortunately, there is no such callback concept in ActiveStorage. While looking the RailsGuide I found something interesting


It's important to know that the file is not yet available in the `after_create` callback but in the `after_create_commit` only.

This looks interesting.

##### Rails Guide Says:
``
  after_create(*args, &block) => Registers a callback to be called after a record is created.
``

``
  after_create_commit(*args, &block) => This callback is called after a record has been created
``

Both look similar, right?

#### So, what made the difference in my codebase?
Your code doesn't execute until after the outermost transaction has been committed when using `after_create_commit`. If you wanted to make many changes in a single transaction, you could use the existing transaction rails or one you developed.

Your `create/save` may still be rolled back at the time `after_save/create` executes, and (by default) it won't be accessible to other database connections, file upload (such as a background process like sidekiq). Using `after_create_commit` is typically driven by one of these two factors in some combination.


#### References
<https://pusher.com/ >  
<https://guides.rubyonrails.org/active_storage_overview.html#downloading-files>  
<https://stackoverflow.com/questions/33890458/difference-between-after-create-after-save-and-after-commit-in-rails-callbacks>
