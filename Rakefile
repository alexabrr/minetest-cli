require "bundler/gem_tasks"
require 'github_changelog_generator/task'
require './lib/helpers/file_helper'
task :default => :spec

GitHubChangelogGenerator::RakeTask.new :changelog_gen do |config|
	config.user = 'alexabrr'
	config.project = 'minetest-cli'
	config.future_release = 'v1.0'
	config.release_branch = 'master'
	config.date_format = '%d-%m-%Y'
	config.header = "# Minetest Changes Log."
	config.simple_list = true
end

Rake::Task['changelog_gen'].clear_comments

desc 'Compile the changelog file from github commits, issues, etc..'
task :changelog do
	Rake::Task['changelog_gen'].invoke
	helper = Minetest::Helpers::FileHelper.new
	helper.remove_lines("CHANGELOG.md", 9, 1)
	helper.append_lines("CHANGELOG.md", "Copyright © 2020 Alex Abreu")
end

task :console do
	require 'irb'
	require 'irb/completion'
	require 'minetest/cli' # Aponta para o start file da aplicação
	
	def reload!
		
		files = $LOADED_FEATURES.select { |feat| feat =~ /\/my_gem\// }
		files.each {  |file| load file }
	end
	
	ARGV.clear
	IRB.start
end