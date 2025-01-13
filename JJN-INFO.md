# JJN-INFO: GIT-CLONE-ORGANIZATION

---

## **What It Does**
- This is a lightweight utility for cloning all repos from a GitHub organization in one go.  
- Handy when I need to bulk clone repos for audits, migrations, or local exploration.  
- Works with 2FA by using a personal access token (PAT). Minimal setup, no frills, and very straightforward.  

---

## **Folder Layout**

```plaintext
/Users/jasonnathan/Repos/git-clone-organization
├── README.md           # Basic usage guide
└── git_clone_org       # The script itself, written in Node.js
```

---

## **How It Works**

### The Script
- It’s an interactive CLI:
  1. **Prompts** for the organization name, destination path, and PAT.  
  2. **Uses `curl`** to fetch all repos in the organization via the GitHub API.  
  3. Loops through the repo list and clones each one via `git clone` using the `ssh_url`.

### Key Features
- **Organization Name Prompt**:  
  Asks for the org name and uses it to query the GitHub API.  
- **Path Selection**:  
  Lets me set a custom destination directory (defaults to current working directory).  
- **Token Authentication**:  
  Supports GitHub’s PATs for accessing private org data and cloning.  
- **Batch Cloning**:  
  Automatically loops through all repos and clones them without manual intervention.  

---

## **How to Use**

### Prerequisites
- **Node.js**: Required to run the script.  
- **GitHub Personal Access Token**:
  - Go to [GitHub’s token page](https://github.com/settings/tokens).  
  - Generate a PAT with `repo` permissions for private repos or `read:org` for public ones.  

### Running It
1. Clone this repo locally:
   ```bash
   git clone git@github.com:richgilbank/git-clone-organization.git
   cd git-clone-organization
   ```

2. Make the script executable:
   ```bash
   chmod +x git_clone_org
   ```

3. Run the script:
   ```bash
   ./git_clone_org
   ```

4. Follow the prompts:
   - Enter the **org name**.
   - Specify the **destination path** (or press Enter for the current directory).  
   - Provide the **personal access token** for authentication.  

---

## **What I Like**
- **Dead Simple**: No dependencies, just plain Node.js and `curl`.  
- **Quick Setup**: Minimal friction for getting all repos locally.  
- **Interactive Flow**: The prompts make it feel user-friendly without needing arguments or flags.  

---

## **Things to Improve**
1. **Error Handling**:  
   - If the token is invalid or the org name doesn’t exist, it just fails silently or throws generic errors. Could use better feedback here.  
2. **Pagination Support**:  
   - GitHub API paginates results after 30 repos. This script will miss repos if the org has more than 30. Adding pagination would make it more robust.  
3. **Verbose Output**:  
   - A simple log of cloned repos, skipped repos, or errors at the end would make it easier to review what happened.  
4. **Parallel Cloning**:  
   - Right now, it clones repos sequentially. Running clones in parallel (e.g., 3-5 at a time) would speed up the process for large orgs.

---

## **Quick Commands**
- **Run the Script**:
  ```bash
  ./git_clone_org
  ```
- **Reset Permissions** (if it doesn’t run):
  ```bash
  chmod +x git_clone_org
  ```

---

## **Repo Link**
```plaintext
origin	git@github.com:richgilbank/git-clone-organization.git
```

---

## **Final Thoughts**
It’s not a critical tool, but it’s definitely nice to have. When I want all repos from an org for a quick audit or local backups, this does the job without fuss. There’s room to improve if I ever feel like it, but for now, it’s perfect for occasional use.
