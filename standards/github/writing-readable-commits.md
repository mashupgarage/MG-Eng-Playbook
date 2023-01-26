# Writing Readable Commits

## Use proper syntax
- Capitalize first letter
- Limit commit subject to 50 characters
- No periods at the end of the commit
- Be consistent
- There are several patterns that are recommended
	- 3rd person singular verb - Improves class names
	- imperative - Improve class names
	- past tense - Improved class names
- Try to stick with one style consistently as much as possible within the same PR
- Adjust accordingly based on team preference or conventions

## Make them as specific as possible
- ❌ Code review
- ❌ Fixes bug
- ✅ Improves implementation of comments
- ✅ Fixes spacing in pdf file
- ✅ Adds tests for invoice approval

## Make them atomic
- Prefer many small and focused commits rather than a few big ones
- Atomic commits can help give a clearer step by step process of what was done
- Atomic commits also help trace changes clearly
- ❌ Implements drag and drop uploads
- ✅ Installs react-dropzone
- ✅ Configures dropzone
- ✅ Adds dropzone to uploader component
- ✅ Validates uploaded files
