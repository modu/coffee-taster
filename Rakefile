require 'rake'
require 'stringio'
require 'coffee-script'

desc "Watch coffee directory and regenerate JavaScript when files change."
task :watch do
  require 'fssm'
  require 'coffee-script'
  puts "Starting to watch CoffeeScript files in /coffee."
  FSSM.monitor("coffee", '**/*.coffee') do
    update { |base, relative| recompile_coffee }
    delete { |base, relative| recompile_coffee }
    create { |base, relative| recompile_coffee }
  end
end

def recompile_coffee
  puts "Changes detected, recompiling"
  code = StringIO.new
  Dir.glob("coffee/**/*.coffee").each do |f|
    code << IO.read(f)
  end
  f = File.new('main.js', 'w')
  f.write CoffeeScript.compile code.string
  f.close
  puts "Recompiled."
end