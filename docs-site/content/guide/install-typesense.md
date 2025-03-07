# Install Typesense

Here are a couple of available options to install and run Typesense.

## Option 1: Typesense Cloud

The easiest way to run Typesense is using our managed Cloud service called [Typesense Cloud](https://cloud.typesense.org/). 

- Sign-in with GitHub 
- Pick a configuration and click on Launch. You'll have a ready-to-use cluster in a few minutes.
- Then click on "Generate API Key", which will give you the hostnames and API keys to use in your code.

## Option 2: Local Machine / Self-Hosting

You can also run Typesense on your local machine or self-host it.

You'll find DEB, RPM and pre-built binaries for Linux (X86_64) and macOS on our [downloads](https://typesense.org/downloads) page.

We also publish official Docker images for Typesense on [Docker hub](https://hub.docker.com/r/typesense/typesense/).

### 📥 Download & Install

#### Mac via Homebrew

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code>brew install typesense/tap/typesense-server@{{ $site.themeConfig.typesenseLatestVersion }}
</code></pre>

  </template>
</Tabs>

#### Mac Binary

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code>curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-darwin-amd64.tar.gz
tar -xzf typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-darwin-amd64.tar.gz
</code></pre>

  </template>
</Tabs>

#### Linux Binary

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code># x64
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-linux-amd64.tar.gz
tar -xzf typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-linux-amd64.tar.gz

# arm64
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-linux-arm64.tar.gz
tar -xzf typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-linux-arm64.tar.gz
</code></pre>

  </template>
</Tabs>


#### Docker

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code>docker pull typesense/typesense:{{ $site.themeConfig.typesenseLatestVersion }}
</code></pre>

  </template>
</Tabs>

#### Docker Compose

<Tabs :tabs="['yml']">
  <template v-slot:yml>

<pre class="language-yaml"><code>version: '3.4'
services:
  typesense:
    image: typesense/typesense:0.24.0
    restart: on-failure
    ports:
      - "8108:8108"
    volumes:
      - ./typesense-data:/data
    command: '--data-dir /data --api-key=xyz --enable-cors'
</code></pre>

  </template>
</Tabs>

```shell
docker-compose up
```

#### DEB package on Ubuntu/Debian

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code># x64
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-amd64.deb
sudo apt install ./typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-amd64.deb

# arm64
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-arm64.deb
sudo apt install ./typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-arm64.deb
</code></pre>

  </template>
</Tabs>

#### RPM package on CentOS/RHEL
<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code># x64
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-1.x86_64.rpm
sudo yum install ./typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-1.x86_64.rpm

# arm64
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-1.arm64.rpm
sudo yum install ./typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-1.arm64.rpm
</code></pre>

  </template>
</Tabs>

#### Windows  [(WSL)](https://docs.microsoft.com/en-us/windows/wsl/install)

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code>wsl
curl -O https://dl.typesense.org/releases/{{ $site.themeConfig.typesenseLatestVersion }}/typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-amd64.deb
sudo apt install ./typesense-server-{{ $site.themeConfig.typesenseLatestVersion }}-amd64.deb
</code></pre>
Note: Post install you would see the message "installed typesense-server package post-installation script subprocess returned error exit status 1"
ignore this error message , executing `apt list --installed | grep typesense` would show that installation was successfull.

  </template>
</Tabs>

### 🎬 Start

#### From Homebrew on macOS

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code>brew services start typesense-server@{{ $site.themeConfig.typesenseLatestVersion }}
</code></pre>

  </template>
</Tabs>

For macOS running on Intel:
- The default API key is `xyz` and the default port is `8108`
- The config file is at `/usr/local/etc/typesense/typesense.ini`
- Logs are under `/usr/local/var/log/typesense/`
- Data dir is under `/usr/local/var/lib/typesense/`

For macOS running on Apple silicon:
- The default API key is `xyz` and the default port is `8108`
- The config file is at `/opt/homebrew/etc/typesense/typesense.ini`
- Logs are under `/opt/homebrew/var/log/typesense/`
- Data dir is under `/opt/homebrew/var/lib/typesense/`

#### From the pre-built binary
If you downloaded the pre-built binary for Mac / Linux, you can start Typesense with minimal options like this:

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

```bash
export TYPESENSE_API_KEY=xyz
mkdir $(pwd)/typesense-data # Use a directory like /var/lib/typesense in production
./typesense-server --data-dir=$(pwd)/typesense-data --api-key=$TYPESENSE_API_KEY --enable-cors
```

  </template>
</Tabs>

#### From the Docker image
If you want to use Docker, you can run Typesense like this:

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

<pre class="language-bash"><code>export TYPESENSE_API_KEY=xyz

mkdir $(pwd)/typesense-data

docker run -p 8108:8108 -v$(pwd)/typesense-data:/data typesense/typesense:{{ $site.themeConfig.typesenseLatestVersion }} \
  --data-dir /data --api-key=$TYPESENSE_API_KEY --enable-cors</code></pre>

  </template>
</Tabs>

#### From DEB / RPM package

If you had installed Typesense from a DEB/RPM package, the Typesense server is automatically started as a systemd service when installation is complete. You can check the status via:

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

```bash
sudo systemctl status typesense-server.service
```

  </template>
</Tabs>

- The config file is at `/etc/typesense/typesense-server.ini`
  - The admin API key is auto-generated and can be found inside the config file. 
- Logs are under `/var/log/typesense/`
- Data dir is under `/var/lib/typesense/`

#### Windows 10 (WSL)
Typesense server can be started by logging into WSL and executing the below given command.

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

```bash
sudo /usr/bin/./typesense-server --config=/etc/typesense/typesense-server.ini
```

  </template>
</Tabs>

You can retrieve the hostname for the server on which Typesense is running using `wsl hostname -I` in cmd.
**You should be able to connect to this hostname/IP address directly from Windows**.

If you'd like Typesense to be started at startup, you can create a BAT file with the command `powershell.exe /c wsl.exe sudo /usr/bin/./typesense-server --config=/etc/typesense/typesense-server.ini` and set it to execute at startup.

By default, Typesense will start on port 8108, and the installation will generate a random API key, which you can view/change from the [configuration file](./configure-typesense.md#using-a-configuration-file) at `/etc/typesense/typesense-server.ini`

:::tip
We are starting a single node here, but Typesense can also run in a clustered mode. See the [High Availability](./high-availability.md) section for more details.
:::

### 🆗 Health Check

You can use the `/health` API end-point to verify that the server is ready to accept requests.

<Tabs :tabs="['Shell']">
  <template v-slot:Shell>

```bash
curl http://localhost:8108/health
{"ok":true}
```

  </template>
</Tabs>

### ⚙️ Configure Typesense

You can configure various Typesense Server settings using command line arguments. 
Read this reference article for more information on 
<RouterLink :to="`/${this.$site.themeConfig.typesenseLatestVersion}/api/server-configuration.html`">How To Configure Typesense Server</RouterLink>.
