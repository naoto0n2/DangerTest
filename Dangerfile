# Include specific word in xib/storyboard
fail_texts = [
  "misplaced=\"YES\"", 
  "calibratedRGB"
]
git.diff.each do |file|
  unless file.path.match(/Dangerfile/)
    fail_texts.map do |fail_text|
      fail "Include `#{fail_text}` in #{file.path}" if /^\+.*#{fail_text}/.match(file.patch)
    end
  end
end

# Include merge commit
if git.commits.any? { |c| c.message =~ /^Merge branch 'master'/ }
  fail 'Please rebase to get rid of the merge commits in this PR'
end

# Commit message does not start with commit mark
if git.commits.any? { |c| c.message =~ /^(?!(:.*:|Revert)).*$/ }
  message c.message
  fail 'Commit message does not start with commit mark'
end

# Include review commit
if git.commits.any? { |c| c.message =~ /\[([sS]elf )?[rR]eview\]/ }
  fail 'Include review commit'
end
