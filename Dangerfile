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

# Check commit message
git.commits.each do |c|
  # Skip merge commit
  next if c.message.start_with?('Merge pull request')

  # Skip revert commit
  next if c.message.start_with?('Revert')

  # Include merge commit
  if c.message.start_with?("Merge branch 'master'")
    fail 'Please rebase to get rid of the merge commits in this PR'
    next
  end

  # Commit message does not start with commit mark
  if c.message =~ /^(?!:.*:).*$/
    fail 'Commit message does not start with commit mark'
    next
  end
end
