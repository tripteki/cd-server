<h1 align="center">Convention</h1>

Trip Teknologi's Continuous Delivery and Continuous Deployment Server Convention.

Getting Started
---

How to use :

- *Optionally* in your own running :<br />`ssh-keygen -t rsa -b 4096 -a 100 -o -f ~/.ssh/id_rsa`.

- *Optionally* in your own running :<br />`ssh-keyscan -t rsa -p <port> -H <host> >> ~/.ssh/known_hosts`.

- You need to publish your publickey to server's `~/.ssh/authorized_keys` with running :<br />`ssh-copy-id -i ~/.ssh/id_rsa.pub -p <port> <user>@<host>`.

- You need to create a workflow in `.github/workflows/`.

    Sample file :

    ```
    name: Continuous Delivery and Continuous Deployment Server

    on: push

    jobs:
        cd:
            runs-on: ubuntu-latest
            steps:
                - uses: tripteki/cd-server@1.0.0
                  with:
                    token: ${{ secrets.GITHUB_TOKEN }}
                    credential: |
                      "host": ${{ secrets.SERVER_HOST }},
                      "port": ${{ secrets.SERVER_PORT }},
                      "user": ${{ secrets.SERVER_USER }},
                      "privatekey": ${{ secrets.SERVER_PRIVATE_KEY }},
                      "privatekey_passphrase": ${{ secrets.SERVER_PRIVATE_KEY_PASSPHRASE }},
                      "path": ${{ secrets.PATH }}
                    type: ssh
                - uses: tripteki/cd-server@1.0.0
                  with:
                    token: ${{ secrets.GITHUB_TOKEN }}
                    credential: |
                      "host": ${{ secrets.SERVER_HOST }},
                      "port": ${{ secrets.SERVER_PORT }},
                      "user": ${{ secrets.SERVER_USER }},
                      "privatekey": ${{ secrets.SERVER_PRIVATE_KEY }},
                      "privatekey_passphrase": ${{ secrets.SERVER_PRIVATE_KEY_PASSPHRASE }},
                      "script": APP_ENV=production ./bin/project -b -l -t -e -c
                    type: command
    ```

- `type` section value possibilities :<br />`ssh`, `command`.
- `artifact` section value possibilities :<br />`composer.json`, `package.json`, `pyproject.toml`, etc.

Author
---

- Trip Teknologi ([@tripteki](https://linkedin.com/company/tripteki))
- Hasby Maulana ([@hsbmaulana](https://linkedin.com/in/hsbmaulana))
