desc 'Build site'
task :build do
  system('jekyll')
end

desc 'Build and deploy'
task :deploy => :build do
  sh 'rsync -rtzh --progress --delete _site/ doozer:~/jekyll/jimbalaya.us/site'
  sh 'rsync -rtzh --progress --delete _audio/ doozer:~/jekyll/jimbalaya.us/audio'
end

desc 'Run Jekyll with --server --auto'
task :dev do
  system('jekyll --server --auto')
end

desc 'List all draft posts'
task :drafts do
  puts `find ./_posts -type f -exec grep -H 'published: false' {} \\;`
end

desc 'Create a new draft post; needs title=TITLE'
task :post do
  title = ENV['title']
  slug = "#{Time.now.strftime('%Y-%m-%d')}-#{title.downcase.gsub(/[^[:alnum:]]+/, '-')}"

  file = File.join(
    File.dirname(__FILE__),
    '_posts',
    slug + '.html'
  )

  File.open(file, "w") do |f|
    f << <<-EOS.gsub(/^    /, '')
    ---
    layout: post
    title: #{title}
    published: false
    categories:
    ---

    EOS
  end

  system ("#{ENV['EDITOR']} #{file} &")
end
