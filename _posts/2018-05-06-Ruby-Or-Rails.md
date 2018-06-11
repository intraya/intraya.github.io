# Summing Up & Division

## Ruby
<pre><code>
arr = [2, 3, 4, 5]
arr.inject {|sum, el| sum + el}.to_f / arr.size
# => 3.5
arr.reduce(:+).to_f / arr.size
# => 3.5
arr.sum.fdiv(arr.size) # higher than ruby 2.4
# => 3.5
</code></pre>

## Rails
<pre><code>
arr = [10, 10, 10, 10]
arr.sum.to_f / arr.size
# => 3.5
</code></pre>

# Precision

## Ruby
<pre><code>
f = 2.0 / 3
# => 0.6666666666666666
f.round(2)
# => 0.67
sprintf("%0.02f", f)
# => "0.67"
"%5.2f" % [2.0/3.0]
# => " 0.67"
</code></pre>

# Make Directory
## Ruby
### FileUtils
<pre><code>
require 'fileutils'
FileUtils::mkdir_p 'foo/bar'
# => ["foo/bar"]
</code></pre>
### System Call
<pre><code>
system 'mkdir', '-p', 'foo/bar' # TODO: Shell Injection Attack Possible?
</code></pre>

# Auto-loading lib files in Rails 4
## Rails
1. with nameing conventions
in config/application.rb
<pre><code>
config.autoload_paths << Rails.root.join('lib') # TODO: rails 3/4
config.eager_load_paths << Rails.root.join('lib') # TODO: rails 5
</code></pre>
in lib/foo.rb:
<pre><code>
class Foo
end
</code></pre>
in lib/foo/bar.rb:
<pre><code>
class Foo::Bar
end
</code></pre>
2. without naming conventions file lib/extensions.rb
in config/initializers/require.rb:
<pre><code>
rquire "#{Rails.root}/lib/extensions"
</code></pre>
## Rails 5
put files under app such as app/services/ or app/presenters/ # TODO

# Regex - " to ""
## Ruby
<pre><code>
# AS-IS
test,first,line,"you are a "kind" man",thanks
again,second,li,"my "boss" is you",good
# TO-BE
test,first,line,"you are a ""kind"" man",thanks
again,second,li,"my ""boss"" is you",good
</code></pre>

<pre><code>
csv = <<ENDCSV
test,first,line,"you are a "kind" man",thanks
again,second,li,"my "boss" is you",good
more,""Someone" said that you're "cute"",yay
"watch out for this",and,also,"this test case"
ENDCSV

puts csv.gsub(/(?<!^|,)"(?!,|$)/,'""')
</code></pre>

* (?<!^|,) --
