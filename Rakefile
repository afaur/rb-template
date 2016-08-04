require "bundler"

Bundler.setup
Bundler::GemHelper.install_tasks

require 'rake'
require 'cucumber/rake/task'
require 'rake/testtask'

task :default => %w(all)

desc 'Run One Minitest Test'
task :test => %w(one)

desc 'Run All Minitest Tests'
task :tests => %w(all)

desc 'Run Cucumber Tests'
task :cuke => %w(features)

task :one do
  tests = []
  tests.each_with_index {|option,i| puts "#{i+1}) #{option}" }
  puts "Which should run?"
  STDOUT.flush
  selection = STDIN.gets.chomp.to_i
  Rake::TestTask.new(:one) do |t|
    t.test_files = FileList["test/#{tests[selection-1]}"]
    t.verbose = true
  end
end

task :all do
  Dir.new('test').each do |f|
    next if f.start_with? '.'
    next if f.start_with? 'support'
    Rake::TestTask.new(:all) do |t|
      t.test_files = FileList["test/#{f}"]
      t.verbose = true
    end
  end
end

task :features do
  Cucumber::Rake::Task.new(:features) do |t|
    t.cucumber_opts = "--format pretty"
  end
end
