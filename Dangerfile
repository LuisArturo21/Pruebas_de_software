# Dangerfile

warn("No PR description provided.") if github.pr_body.empty?

# Get all commits in the PR
github.commits.each do |commit|
  lines = commit.commit.message.lines

  title = lines.first.strip
  description = lines[1..].map(&:strip).reject(&:empty?)

  # Check title length
  if title.length > 50
    fail("Commit title exceeds 50 characters: '#{title}'")
  end

  # Check for empty line after title
  if lines.length > 1 && lines[1].strip != ""
    fail("Commit message must have an empty line between title and description.")
  end

  # Check description length
  if description.any? && description.join.length < 5
    fail("Commit description must be at least 5 characters long.")
  end

  # Check max length per line in description
  description.each do |line|
    if line.length > 72
      fail("Commit description line exceeds 72 characters: '#{line}'")
    end
  end
end
