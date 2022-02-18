# Chirpy

🌏 English • [简体中文](docs/README_zh-CN.md)

[![Build Status](https://github.com/cotes2020/jekyll-theme-chirpy/workflows/build/badge.svg?branch=master&event=push)](https://github.com/cotes2020/jekyll-theme-chirpy/actions?query=branch%3Amaster+event%3Apush)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/8220b926db514f13afc3f02b7f884f4b)](https://app.codacy.com/manual/cotes2020/jekyll-theme-chirpy?utm_source=github.com&utm_medium=referral&utm_content=cotes2020/jekyll-theme-chirpy&utm_campaign=Badge_Grade_Dashboard)
[![GitHub license](https://img.shields.io/github/license/cotes2020/jekyll-theme-chirpy.svg)](https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/LICENSE)
[![996.icu](https://img.shields.io/badge/link-996.icu-%23FF4D5B.svg)](https://996.icu)

A minimal, sidebar, responsive web design Jekyll theme, focusing on text presentation, aim to help you easily record and share your knowledge.. [Live Demo »](https://chirpy.cotes.info)

[![Devices Mockup](https://raw.githubusercontent.com/cotes2020/jekyll-theme-chirpy/master/assets/img/sample/devices-mockup.png)](https://chirpy.cotes.info)

## Table of Contents

- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)
- [Credits](#credits)
- [Support](#support)
- [License](#license)

## Features

- Pinned Posts
- Configurable theme mode
- Double-level Categories
- Last modified date for posts
- Table of Contents
- Automatically recommend related posts
- Syntax highlighting
- Mathematical expressions
- Search
- Atom Feeds
- Disqus Comments
- Google Analytics
- GA Pageviews reporting (Advanced)
- SEO and Performance Optimization

## Installation

[Fork **Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/fork) on GitHub, rename the repository to `USERNAME.github.io` (where `USERNAME` is your GitHub username), and then open terminal and clone the fork to local by:

```terminal
$ git clone https://github.com/USERNAME/USERNAME.github.io.git -b master --single-branch
```

### Setting up the local envrionment

If you would like to run or build the project on your local machine, please follow the [Jekyll Docs](https://jekyllrb.com/docs/installation/) to complete the installation of `Ruby`, `RubyGems` and `Bundler`. 

Before running or building for the first time, please complete the installation of the Jekyll plugins. Go to the root directory of project and run:

```terminal
$ bundle install
```

`bundle` will automatically install all the dependencies specified by `Gemfile`.

In order to generate some extra files (_categories_, _tags_ and _last modified list_), we need to use some tool scripts. And they require dependency package [yq](https://github.com/mikefarah/yq#install) to be installed. What's more, if your machine is running Debian or macOS, you also need to install [GNU coreutils](https://www.gnu.org/software/coreutils/).

- on Debian:

  ```console
  $ sudo apt-get install coreutils
  ```

- on macOS:

  ```console
  $ brew install coreutils
  ```

### Setting up Docker environment (optional)

If you're a loyal fan of [**Docker**](https://www.docker.com/) or just too lazy to install the packages mentioned in [_Setting up the local envrionment_](#setting-up-the-local-envrionment), please make sure you have **Docker Engine** installed and running, and then get Docker image `jekyll/jekyll` from Docker Hub by the following command:

```console
$ docker pull jekyll/jekyll:latest
```

## Usage

Running [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/) requires some extra files, which cannot be generated by Jekyll native commands, so please strictly follow the methods mentioned below to run or deploy your website.

### Initialization

Go to the root directory of the project and start initialization:

```console
$ bash tools/init.sh
```

> **Note**: If you not intend to deploy it on GitHub Pages, append parameter option `--no-gh` at the end of the above command.

What it does is:

1. Remove some files or directories from your repository:

    - `.travis.yml`
    - files under `_posts`
    - folder `docs`

2. If you use the `--no-gh` option, the directory `.github` will be deleted. Otherwise, setup the GitHub Action workflow by removing extension `.hook` of `.github/workflows/pages-deploy.yml.hook`, and then remove the other files and directories in folder `.github`. 

3. Automatically create a commit to save the changes.

### Configuration

Generally, go to `_config.yml` and configure the variables as needed. Some of them are typical options:

- `url`
- `avatar`
- `timezone`
- `theme_mode`

### Run Locally

You may want to preview the site contents before publishing, so just run it by:

```terminal
$ bash tools/run.sh
```

Then open a browser and visit to <http://localhost:4000>.

Few days later, you may find that the file changes does not refresh in real time by using `run.sh`. Don't worry, the advanced option `-r` (or `--realtime`) will solve this problem, but it requires [**fswatch**](http://emcrisostomo.github.io/fswatch/) to be installed on your machine.

### Run on Docker

Run the site on Docker with the following command:

```terminal
$ docker run --rm -it \
    --volume="$PWD:/srv/jekyll" \
    -p 4000:4000 jekyll/jekyll \
    bash tools/run.sh --docker
```

Please note that on Docker containers, you'll lose the real-time refresh feature.

### Deployment

Before the deployment begins, checkout the file `_config.yml` and make sure the `url` is configured correctly. Furthermore, if you prefer the [_project site_](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites) and don't use a custom domain, or you want to visit your website with a base url on a web server other than **GitHub Pages**, remember to change the `baseurl` to your project name that starting with a slash. For example, `/project`.

Assuming you have already gone through the [initialization](#initialization), you can now choose ONE of the following methods to deploy your website.

#### Deploy on GitHub Pages

For security reasons, GitHub Pages build runs on `safe` mode, which restricts us from using tool scripts to generate additional page files. Therefore, we can use **GitHub Actions** to build the site, store the built site files on a new branch, and use that branch as the source of the Pages service.

1. Push any commit to `origin/master` to trigger the GitHub Actions workflow. Once the build is complete and successful, a new remote branch named `gh-pages` will appear to store the built site files.

2. Browse to your repository on GitHub and choose the branch `gh-pages` as the [publishing source](https://docs.github.com/en/github/working-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site) throught _Settings_ → _Options_ → _GitHub Pages_:
    ![gh-pages-sources](https://raw.githubusercontent.com/cotes2020/jekyll-theme-chirpy/master/assets/img/sample/gh-pages-sources.png)

3. Visit your website at the address indicated by GitHub.

#### Deploy on Other Platforms

On platforms other than GitHub, we cannot enjoy the convenience of **GitHub Actions**. Therefore, we should build the site locally (or on some other 3rd-party CI platform) and then put the site files on the server.

Go to the root of the source project, build your site by:

```console
$ bash tools/build.sh
```

> **Note**: The output path can be specified with the option `-d`.

Or, build the site with Docker by:

```terminal
$ docker run --rm -it \
    --volume="$PWD:/srv/jekyll" \
    jekyll/jekyll \
    bash tools/build.sh --docker
```

Unless you specified the output path, the generated site files will be placed in folder `_site` of the project's root directory. Now you should upload those files to your web server.

### Documentation

For more details and the better reading experience, please check out the [tutorials on demo site](https://chirpy.cotes.info/categories/tutorial/). In the meanwhile, a copy of the tutorial is also available on the [Wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki).

## Contributing

The old saying, "Two heads are better than one." Consequently, welcome to report bugs, improve code quality or submit a new feature. For more information, see [contributing guidelines](.github/CONTRIBUTING.md).

## Credits

This theme is mainly built with [Jekyll](https://jekyllrb.com/) ecosystem, [Bootstrap](https://getbootstrap.com/), [Font Awesome](https://fontawesome.com/) and some other wonderful tools (their copyright information can be found in the relevant files).

:tada: Thanks to all the volunteers who contributed to this project, their GitHub IDs are on [this list](https://github.com/cotes2020/jekyll-theme-chirpy/graphs/contributors). Also, I won't forget those guys who submitted the issues or unmerged PR because they reported bugs, shared ideas or inspired me to write more readable documentation.

## Support

If you enjoy this theme or find it helpful, please consider becoming my sponsor, I'd really appreciate it! Click the button <kbd>:heart: Sponsor</kbd> at the top of the [Home Page](https://github.com/cotes2020/jekyll-theme-chirpy) and choose a link that suits you to donate; this will encourage and help me better maintain the project.

## License

This work is published under [MIT](https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/LICENSE) License.
