## Simply Web Restart
Restart your web application pool on Simply.com or any other place that supports IIS using this GitHub action. 

---

### Example
Place the following in `/.github/workflows/main.yml`
```yml
name: Restart application on Simply

on:
  workflow_dispatch:

jobs:
  restart:
    name: Restart application on Simply
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4

      - name: Restart application
        uses: rasmusbuchholdt/simply-web-restart@1.0.0
        with:
          website-name: ${{ secrets.WEBSITE_NAME }}
          server-computer-name: ${{ secrets.SERVER_COMPUTER_NAME }}
          server-username: ${{ secrets.SERVER_USERNAME }}
          server-password: ${{ secrets.SERVER_PASSWORD }}
```

---

### Requirements
- Administrator access to the simply.com account, to access the required credentials.

---

### Setup
1. Locate the repository you want to automate Simply web deployment in.
2. Select the `Actions` tab.
3. Select `Set up a workflow yourself`.
4. Copy paste one of the examples into your .yml workflow file and commit the file.
5. All the examples takes advantage of `Secrets`, so make sure you have added the required secrets to your repository. Instructions on this can be found in the [settings](#settings) section.
6. Once you have added your secrets, your new workflow should be running on every push to the branch.

---

### Settings
These settings can be either be added directly to your .yml config file or referenced from your GitHub repository `Secrets`. I strongly recommend storing any private values like `server-username` and `server-password` in `Secrets`, regardless of if the repository is private or not.

To add a secret to your repository go to the `Settings` tab, followed by `Secrets`. Here you can add your secrets and reference to them in your .yml file.

| Setting | Required | Example | Default Value | Description |
|-|-|-|-|-|
| `website-name`          | Yes | `sub.example.com` | | Deployment destination server |
| `server-computer-name`  | Yes | `https://nt8.unoeuro.com:8172` | | Computer name, including the port - Find yours [here](https://www.simply.com/dk/support/faq/asp/236/)|
| `server-username`       | Yes | `username`        | | Your Simply FTP username |
| `server-password`       | Yes | `password`        | | Your Simply FTP password |