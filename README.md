# Docker Image for git-quick-stats, by [FEROX](https://ferox.yt)

![Docker Cloud Automated build](https://img.shields.io/docker/cloud/automated/frxyt/docker-git-quick-stats.svg)
![Docker Cloud Build Status](https://img.shields.io/docker/cloud/build/frxyt/git-quick-stats.svg)
![Docker Pulls](https://img.shields.io/docker/pulls/frxyt/git-quick-stats.svg)
![GitHub issues](https://img.shields.io/github/issues/frxyt/docker-git-quick-stats.svg)
![GitHub last commit](https://img.shields.io/github/last-commit/frxyt/docker-git-quick-stats.svg)

This image packages [`git-quick-stats`](https://github.com/arzzen/git-quick-stats).

* Docker Hub: https://hub.docker.com/r/frxyt/git-quick-stats
* GitHub: https://github.com/frxyt/docker-git-quick-stats

## Docker Hub Image

**`frxyt/git-quick-stats`**

## Usage

* Run it in a git enabled repository: 
  * Unix: `docker run --rm -it -v $(pwd):$(pwd):ro frxyt/git-quick-stats`
  * Windows: `docker run --rm -it -v %cd%:/git:ro frxyt/git-quick-stats`
* Run it on Gitlab CI by adding to your `.gitlab-ci.yml` file:
  ```yaml
  build:stats:
    image: frxyt/git-quick-stats
    stage: build
    script:
      - export _GIT_MONTH=$(git show -s --format=%ci -1 | cut -d'-' -f1-2)
      - export _GIT_SINCE=${_GIT_MONTH}-01
      - export _GIT_UNTIL=${_GIT_MONTH}-$(cal 01 ${_GIT_MONTH##*-} ${_GIT_MONTH%%-*} | sed 's/ /\n/g' | grep "\d" | tail -1)
      - echo "Computing git stats from '${_GIT_SINCE}' to '${_GIT_UNTIL}':"
      - git quick-stats -T
      - git quick-stats -r
      - unset _GIT_MONTH _GIT_SINCE _GIT_UNTIL
      - echo "Computing git stats since the first commit:"
      - git quick-stats -T
      - git quick-stats -r
    allow_failure: true
  ```

## Build

```sh
docker build -t frxyt/git-quick-stats .
```

## License

This project and images are published under the [MIT License](LICENSE).

```
MIT License

Copyright (c) 2019 FEROX YT EIRL, www.ferox.yt <devops@ferox.yt>
Copyright (c) 2019 Jérémy WALTHER <jeremy.walther@golflima.net>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```