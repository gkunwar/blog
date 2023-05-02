---
layout: post
permalink: /about/
comments: false
---
{% highlight ruby %}
class Ganesh
  def initialize
    @name = "Ganesh Kunwar"
    @address = {
      country = "Nepal",
      city = "Kathmandu"
    }
    @skills = ['Product Concept Design', 'Product Development', 'Product Scaling']
    @code = {
      backend = ['Ruby', 'Rails', 'Elixir'],
      frontend = ['ReactJS', 'VueJS'],
      database = ['MySQL', 'PostgreSQL', 'MongoDB'],
      cloud = ['AWS', 'Linode']
    },
    @contact = {
      Email = 'gkunwar09@gmail.com',
      Phone = '9801190557'
    },
    @social = {
      twitter = '@gkunwar1',
      linkedin = 'https://www.linkedin.com/in/gkunwar1/',
      github = 'gkunwar'
    },
    @education = ['BE', 'MBA']
  end
end
{% endhighlight %}
