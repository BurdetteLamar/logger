begin
  require "bundler/gem_tasks"
rescue LoadError
end

require "rake/testtask"
Rake::TestTask.new(:test) do |t|
  t.test_files = FileList["test/**/test_*.rb"]
end

require "rdoc/task"
RDoc::Task.new do |doc|
  doc.main   = "README.md"
  doc.title  = "Logger -- Ruby Standard Logger"
  doc.rdoc_files = FileList.new %w[README.md lib LICENSE.txt]
  doc.rdoc_dir = "html"
end

task "gh-pages" => :rdoc do
  %x[git checkout gh-pages]
  require "fileutils"
  FileUtils.rm_rf "/tmp/html"
  FileUtils.mv "html", "/tmp"
  FileUtils.rm_rf "*"
  FileUtils.cp_r Dir.glob("/tmp/html/*"), "."
end

task :sync_tool do
  require 'fileutils'
  FileUtils.cp "../ruby/tool/lib/core_assertions.rb", "./test/lib"
  FileUtils.cp "../ruby/tool/lib/envutil.rb", "./test/lib"
  FileUtils.cp "../ruby/tool/lib/find_executable.rb", "./test/lib"
end

task :default => :test
