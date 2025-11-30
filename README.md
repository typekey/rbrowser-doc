# RBrowser Documentation (`rbrowser-doc`)

This repository contains the **documentation source** for **RBrowser**, an RNA-centric, multi-omics genome & transcriptome browser.

- User guides and tutorials for RBrowser
- Configuration and deployment instructions
- Developer notes and advanced usage examples



## Editing and Contributing

### For Users Without Programming Background

How to collaboratively edit documentation pages?

1. Each page has an edit button in the upper right corner. You can click it directly to edit. ![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472550386-aa4ba7a4-f10e-42d3-b0c7-22a1e2e633dc.png)

2. The first time you edit, you need to fork the current repository. Just click the green button.

![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472215502-497034c8-842b-4c8f-84a5-0171ce34aff1.png)

3. Click the edit button in the upper right corner to enter the editing page. We use Markdown files. You may need to learn about Markdown format, which is quite simple.

![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472254065-495fd295-970a-4897-9fd7-96f1f2290dc7.png)

4. When the modification is complete, click "Commit changes"

![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472294352-b1f3de82-7bfc-49fa-842f-17811976c531.png)

5. Fill in a brief description of the modification on the page. If the review is approved, the modified content will appear directly in the RBrowser Documentation.
   The commit message is required. GitHub will automatically generate some description for the Extended description field.

![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472388354-518522ad-96d3-4cd8-bb2d-190de5315d5b.png)

6. On the source file page of each page, you can see the commit history of that page.

![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472456932-848f6f4e-e11d-4297-a8ac-d97cba4b3f93.png)

7. In the history page, you can see the commit history of that page.

![img](https://cdn.nlark.com/yuque/0/2025/png/1007992/1764472496767-0a57d308-1f3c-4dc7-896b-6bac8f323457.png)

### For Users With Programming Background

If you want to collaborate on editing the documentation, please:

1. **Clone** the repository:

   ```
   git clone https://github.com/typekey/rbrowser-doc.git
   cd rbrowser-doc
   ```

2. **Create a feature branch** (recommended):

   ```
   git checkout -b docs/feature-my-update
   ```

3. **Run the local server** and edit files under `docs/`.

4. **Check that everything builds**:

   ```
   mkdocs build
   ```

5. **Commit your changes**:

   ```
   git status
   git add docs/path/to/changed-file.md
   git commit -m "docs: update XYZ section"
   ```

6. **Push** your branch:

   ```
   git push origin docs/feature-my-update
   ```

7. Open a **Pull Request** against `typekey/rbrowser-doc` on GitHub.

> If you have direct push access and are making small fixes (typos, minor formatting), you may push directly, but using feature branches and pull requests is preferred.



## Prerequisites

To work with this documentation repository, you will need:

- **Python**: Version **3.8+** (recommended 3.9 or newer)
- **pip**: Python package manager
- **git**: To clone and update the repository

Optional but recommended:

- A **virtual environment** tool:
  - `venv` (bundled with Python)
  - or `conda` / `mamba` if you already use them

------

## Run Locally

First, clone the repository:

```
git clone https://github.com/typekey/rbrowser-doc.git
cd rbrowser-doc
```

Then proceed with the instructions for your operating system.

------

## macOS

1. **Create and activate a virtual environment (recommended)**:

   ```
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. **Install dependencies**:

   ```
   pip install -r requirements.txt
   # If requirements.txt is not available, install at least:
   # pip install mkdocs mkdocs-material
   ```

3. **Make the run script executable (first time only)**:

   ```
   chmod +x run.sh
   ```

4. **Start the documentation server**:

   ```
   ./run.sh
   ```

5. **Open your browser and navigate to:**

   ```
   http://localhost:8131
   ```

------

## Linux

1. **Create and activate a virtual environment**:

   ```
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. **Install dependencies**:

   ```
   pip install -r requirements.txt
   # Or: pip install mkdocs mkdocs-material
   ```

3. **Ensure `run.sh` is executable**:

   ```
   chmod +x run.sh
   ```

4. **Start the documentation server**:

   ```
   ./run.sh
   ```

5. **Open your browser and navigate to:**

   ```
   http://localhost:8131
   ```

If you are running on a remote Linux server, you can use SSH port forwarding:

```
ssh -L 8131:localhost:8131 user@your-server
# Then open http://localhost:8131 in your local browser.
```

------

## Windows

1. **Clone the repository and enter the directory**:

   ```
   git clone https://github.com/typekey/rbrowser-doc.git
   cd rbrowser-doc
   ```

2. **Create and activate a virtual environment**:

   ```
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1   # PowerShell
   # or, in CMD:
   # .venv\Scripts\activate.bat
   ```

3. **Install dependencies**:

   ```
   pip install -r requirements.txt
   # Or: pip install mkdocs mkdocs-material
   ```

4. **Run MkDocs directly (instead of run.sh)**:

   ```
   mkdocs serve -a localhost:8131
   ```

5. **Open your browser and navigate to:**

   ```
   http://localhost:8131
   ```

------
## License

The texts, code, images, photos, and videos in this repository are licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

