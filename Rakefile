require 'rake'
require 'rake/gempackagetask'
require 'rake/clean'
require 'rake/testtask'
require 'find'

gem_spec = Gem::Specification.new do |s|
  s.name = 'mollom-patched'
  s.version = '0.1.5.1'
  s.summary = %{mollom-patched}
  s.description = %{mollom-patched was developed by: tflynn}
  s.author = "tflynn"
  s.email = "gems@olioinfo.net"
  #s.homepage = ""

  s.test_files = FileList['test/**/*']

  s.files = FileList['lib/**/*.rb', 'README', 'doc/**/*.*']
  s.require_paths << 'lib'
  
  # This will loop through all files in your lib directory and autorequire them for you.
  # It will also ignore all Subversion files.
  s.autorequire = []

  ["lib"].each do |dir|
    Find.find(dir) do |f|
      if FileTest.directory?(f) and !f.match(/.svn/)
        s.require_paths << f
      else
        if FileTest.file?(f)
          m = f.match(/[a-zA-Z-_]*.rb/)
          if m
            model = m.to_s
            unless model.match("test_")
              x = model.gsub('/', '').gsub('.rb', '')
              s.autorequire << x
            end
          end
        end
      end
    end
  end
  s.autorequire.uniq!

  #s.bindir = "bin"
  #s.executables = "mollom-patched"
  #s.default_executable = ""
  #s.add_dependency("", "")
  #s.add_dependency("", "")
  #s.extensions << ""
  #s.extra_rdoc_files = ["README"]
  #s.has_rdoc = true
  #s.platform = "Gem::Platform::Ruby"
  #s.required_ruby_version = ">= 1.8.5"
  #s.requirements << "An ice cold beer."
  #s.requirements << "Some free time!"
  #s.rubyforge_project = "mollom-patched"
end

Rake::GemPackageTask.new(gem_spec) do |pkg|
  pkg.need_zip = false
  pkg.need_tar = false
  rm_f FileList['pkg/**/*.*']
end

desc "Run test code"
Rake::TestTask.new(:default) do |t|
  t.libs << "test"
  t.pattern = 'test/**/*_test.rb'
  t.verbose = true
end