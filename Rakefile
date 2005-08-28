require 'rake/testtask'
require 'rake/rdoctask'
require 'rake/packagetask'

task :default => [:package]

Rake::TestTask.new do |t|
	t.libs << "test"
	t.test_files = FileList['test/tc_*.rb']
end

Rake::RDocTask.new do |rd|
  f = []
  f << 'lib/xmpp4r.rb'
  f += Dir.glob('lib/xmpp4r/*.rb')
  p f.delete("lib/xmpp4r/xmpp4r.rb")
  # hack to document the Jabber module properly
  f << 'lib/xmpp4r/xmpp4r.rb'
	rd.rdoc_files.include(f)
	rd.options << '--all'
	rd.options << '--diagram'
	rd.options << '--fileboxes'
	rd.options << '--inline-source'
	rd.options << '--line-numbers'
	rd.rdoc_dir = 'rdoc'
end

task :doctoweb => [:rdoc] do |t|
   # copies the rdoc to the CVS repository for xmpp4r website
	# repository is in $CVSDIR (default: ~/dev/xmpp4r-web)
   sh "./doctoweb.bash"
end

Rake::PackageTask.new('xmpp4r', '0.1') do |p|
	p.need_tar = true
	p.package_files.include('ChangeLog', 'README', 'COPYING', 'setup.rb',
	'Rakefile', 'examples/*', 'examples/*/*', 'test/*.rb', 'lib/*.rb',
	'lib/xmpp4r/*.rb', 'lib/xmpp4r/iq/*.rb')
end

