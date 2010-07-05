# encoding: UTF-8

require 'rake'
require 'rake/testtask'
require 'rake/rdoctask'
require File.join(File.dirname(__FILE__), 'lib', 'dm-devise', 'version')

desc 'Run Devise tests using DataMapper. Specify path to devise with DEVISE_PATH'
Rake::TestTask.new(:test) do |test|
  ENV['DEVISE_PATH'] ||= File.expand_path('../devise')
  unless File.exist?(ENV['DEVISE_PATH'])
    puts "Specify the path to devise (e.g. rake DEVISE_PATH=/path/to/devise). Not found at #{ENV['DEVISE_PATH']}"
    exit
  end
  test.libs << 'lib' << 'test'
  test.libs << "#{ENV['DEVISE_PATH']}/lib"
  test.libs << "#{ENV['DEVISE_PATH']}/test"
  # Need to ensure overrides_test is loaded last
  test.test_files = FileList["#{ENV['DEVISE_PATH']}/test/**/*_test.rb"] + ['test/overrides_test.rb']
  test.verbose = true
end

task :test => :check_dependencies

task :default => :test

desc 'Generate documentation for dm-devise.'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_dir = 'rdoc'
  rdoc.title    = 'dm-devise #{version}'
  rdoc.options << '--line-numbers' << '--inline-source'
  rdoc.rdoc_files.include('README.rdoc')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

begin
  require 'jeweler'
  Jeweler::Tasks.new do |gem|
    gem.name = "dm-devise"
    gem.version = DataMapper::Devise::VERSION.dup
    gem.summary = %Q{Support for using DataMapper ORM with devise}
    gem.description = %Q{dm-devise adds DataMapper support to devise (http://github.com/plataformatec/devise) for authentication support for Rails}
    gem.email = "jmorgan@morgancreative.net"
    gem.homepage = "http://github.com/jm81/dm-devise"
    gem.authors = ["Jared Morgan"]
    gem.add_dependency 'dm-core', '~> 1.0.0'
    gem.add_dependency 'dm-migrations', '~> 1.0.0'
    gem.add_dependency 'dm-validations', '~> 1.0.0'
    gem.add_dependency 'dm-serializer', '~> 1.0.0'
    gem.add_dependency 'dm-timestamps', '~> 1.0.0'
    gem.add_dependency 'dm-rails', '~> 1.0.0'
    # gem.add_dependency 'devise', '~> 1.1.0'
    gem.add_dependency("warden", "~> 0.10.7")
    gem.add_dependency("bcrypt-ruby", "~> 2.1.2")
    # gem is a Gem::Specification... see http://www.rubygems.org/read/chapter/20 for additional settings
  end
  Jeweler::GemcutterTasks.new
rescue LoadError
  puts "Jeweler (or a dependency) not available. Install it with: gem install jeweler"
end
