require 'echoe'

Echoe.new("memcached-northscale") do |p|
  p.author = "Sean Lynch"
  p.project = "northscale"
  p.summary = "Test gem. Do not use unless you know what you're doing."
  p.url = "http://blog.evanweaver.com/files/doc/fauna/memcached/"
  p.docs_host = "blog.evanweaver.com:~/www/bax/public/files/doc/"
  p.rdoc_pattern = /README|TODO|LICENSE|CHANGELOG|BENCH|COMPAT|exceptions|behaviors|rails.rb|memcached.rb/
  p.clean_pattern += ["ext/lib", "ext/include", "ext/share", "ext/libmemcached-?.??", "ext/bin", "ext/conftest.dSYM"]
end

task :exceptions do
  $LOAD_PATH << "lib"
  require 'memcached'
  Memcached.constants.sort.each do |const_name|
    const = Memcached.send(:const_get, const_name)
    next if const == Memcached::Success or const == Memcached::Stored
    if const.is_a? Class and const < Memcached::Error
      puts "* Memcached::#{const_name}"
    end
  end
end

task :valgrind do
  exec("valgrind  --tool=memcheck --leak-check=full --show-reachable=no --num-callers=15 --track-fds=yes --workaround-gcc296-bugs=yes --max-stackframe=7304328 --dsymutil=yes --track-origins=yes ruby #{File.dirname(__FILE__)}/test/profile/valgrind.rb")
end

task :profile do
 exec("ruby #{File.dirname(__FILE__)}/test/profile/profile.rb")
end
