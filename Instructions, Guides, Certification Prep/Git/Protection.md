If you want to ensure that no one can accidentally or maliciously push changes to your main branch, you can set up branch protection rules.

### Set Up Branch Protection Rules:
1. Go to the **Settings** tab of your repository.
2. Select **Branches** from the left sidebar.
3. Click on **Add rule** under the **Branch protection rules** section.

### Configure Branch Protection:
1. Specify the branch name pattern (e.g., `main` or `master`).
2. Check **Require a pull request before merging**.
3. Optionally, you can also check:
   - **Require pull request reviews before merging**
   - **Require status checks to pass before merging**
   - **Restrict who can push to matching branches** (Leave this unchecked if only you have write access, otherwise specify who can push)
4. Click **Create** or **Save changes**.
