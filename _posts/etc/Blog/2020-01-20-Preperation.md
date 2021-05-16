---
date: 2020-01-20 23:47
title: GirHub Blog - 설치하기
category: Blog
tags: [github, pages, blog, jekyll]
# published: false
---
{% assign path = page.imgpath | append: page.id %}

- imgpath : {{page.imgpath}}
- pageid : {{page.id}}

# Summary

1. 로컬에 Ruby, Jekyll 설치 및 설정
2. 블로그홈 생성
    1. Jekyll을 이용하여 직접 new home 생성해서 사용하기
    2. Jekyll theme을 이용하여 git clone으로 로컬에 복제하여 custumizing하여 사용하기
3. Gitbuh pages 및 Repository 생성
4. Github Pages에 Git Push해서 웹호스팅

> \[GitHub Pages 참고\]  
> [jekyllrb-ko](https://jekyllrb-ko.github.io/docs/installation/)  
> [블로그 만들기 GitHub 편 총정리](https://blog.chulgil.me/how-to-make-blog-using-github/)  
> [GitHub Pages 블로그 따라하기Permalink](https://devinlife.com/howto/)  

> \[오류 참고\]  
> [Jekyll on macOS](https://jekyllrb.com/docs/installation/macos/) : 결국 이 방법으로 설치하자!!  
> [github.io 만들기 01 - gitpages with jekyll 환경설정](http://dawoonjeong.com/gitpages_with_jekyll_01/)  
> [Installing the Xcode Command Line Tools on a Mac](https://www.embarcadero.com/starthere/berlin/mobdevsetup/ios/en/installing_the_xcode_command_line_tools_on_a_mac.html)

## 준비 사항

- Ruby 2.2.5 이상. 모든 개발환경 헤더 포함 : 루비 설치정보는 ruby -v 로 확인
- RubyGems : 명령어 gem -v 로 확인
- GCC 와 Make : 명령행 인터페이스에서 gcc -v 와 g++ -v, make -v 로 확인

```
$ ruby -v

$ gem -v  

$ gcc -v

$ g++ -v  

$ make -v  
```

# 0\. Homebrew로 상태 확인하기

오류 발생 때문에 뒤져보다보니 새로 설치하기 전 Homebrew로 확인하라고 해서 답답한 마음에 실행해 봄. 그 덕에 Xcode outdated 발견했으니 밑져야 본전. 한 번씩 확인해보자!

- Run '**brew doctor**' before you install anything
- Run '**brew help**' to get started

> **REF** [Homebrew 설치하기](https://imasoftwareengineer.tistory.com/10)

```
$ brew doctor  
Please note that these warnings are just used to help the Homebrew maintainers  
with debugging if you file an issue. If everything you use Homebrew for is  
working fine: please don't worry or file an issue; just ignore this. Thanks!

Warning: "config" scripts exist outside your system or Homebrew directories.  
`./configure` scripts often look for \*-config scripts to determine if  
software packages are installed, and what additional flags to use when  
compiling and linking.

...

Warning: Your Xcode (9.4) is outdated.  
Please update to Xcode 10.2 (or delete it).  
Xcode can be updated from the App Store.
```

# 1\. Xcode

-   Xcode 10.0 이상 (Mac OS Mojave 이상 설치 가능)

```
$xcode-select --install  
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

이미 설치되어 있으나 명령어는 찾을 수 없다고 한다.

### 오류 해결 1) command로 xcode 삭제 및 재설치

-   이 방법으로 해봤는데, Xcode outdated 버전이 설치되었다. 결국 아래 2번 방법으로 재설치했다.

```
$ sudo rm -rf /Library/Developer/CommandLineTools

$ xcode-select --install  
xcode-select: note: install requested for command line developer tools
```

> **REF** [xcode-select: error: command line tools are already installed, use "Software Update" to install updates](https://oneshottenkill.tistory.com/539)

### 오류 해결 2) Xcode App Store 재설치 (Worked!!)

위의 1번 방법으로 명령어로 삭제하고 다시 설치를 해보았다. 하지만 결과는 똑같았다.  
그래서 결국 Applications에서 Xcode를 삭제하고 App Store에서 새로 설치를 진행한 후 'xcode-select --install' 명령어를 재실행하니 설치가 진행된다. 그래도 터미널에서 'xcode -v'를 입력해도 command not found이다.

![Install]({{path}}/img01.png){:width='400px'}  
![Install]({{path}}/img02.png){:width='400px'}  

### Command Line Tools Version 확인

-   Xcode 실행 > Preference > Locations Tab  
    : 2020.1월에 새로 설치했더니 11.3.1 버전이 설치되었다.

![Install]({{path}}/img03.png){:width='600px'}  
*Command Line Tools Version 확인*

# Ruby 설치 및 설정

Mac이라 Ruby가 이미 설치되어 있어서 바로 Jekyll 설치하려했더니 Gem File Permission Error가 발생했다. 내 맥북은 .bash\_profile에 환경설정 추가하게 되어있다. 홈 경로에서 설정 파일 확인해서 추가하면 된다.

## Ruby 설정

```
# 기본 설정
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc  
echo 'export GEM\_HOME=$HOME/gems' >> ~/.bashrc  
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bashrc  
source ~/.bashrc

# 내 맥북 설정
$ echo '# Install Ruby Gems to ~/gems' >> ~/.bash_profile  
$ echo 'export GEM\_HOME=$HOME/gems' >> ~/.bash_profile  
$ echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bash_profile  
$ source ~/.bash_profile
```

> **REF** [https://devinlife.com](https://devinlife.com/howto%20github%20pages/github-prepare/)

### Ruby 재설치

```
$ /usr/bin/ruby -e "$(curl -fsSL [https://raw.githubusercontent.com/Homebrew/install/master/install)"](https://raw.githubusercontent.com/Homebrew/install/master/install)")  

$ brew install ruby
```

## Jekyll과 bundler 설치

역시 또 오류가 발생해있다. 일단 진행해보자.

> I had the same issue on Mac OS Mojave and Xcode 11.2 and unf\_ext 0.0.7.6.  
> To fix it, I downgraded Xcode command line tools to Xcode 10.3 and bundle install worked as expected.

\*내 Xcode 버전은 9.## 인데 안된다. 근데 터미널에서는 xcode 명령어를 인식하지 못한다. 왜지??

```
$ gem install jekyll bundler
Building native extensions. This could take a while...
ERROR:  Error installing jekyll:
    ERROR: Failed to build gem native extension.

$ gem install --user-install bundler jekyll
WARNING:  You don't have /Users/minky/.gem/ruby/2.6.0/bin in your PATH,
      gem executables will not run.
Successfully installed bundler-2.1.4
...
If you are upgrading your Rails application from an older version of Rails:

Please check your Rails app for 'config.i18n.fallbacks = true'.
If you're using I18n (>= 1.1.0) and Rails (< 5.2.2), this should be
'config.i18n.fallbacks = [I18n.default_locale]'.
If not, fallbacks will be broken in your app by I18n 1.1.x.
...
24 gems installed
```

### sudo 권한으로 설치 강력 권장

```
$ sudo gem install bundler
  
$ sudo gem install -n /usr/local/bin/ jekyll
```

# 기본 블로그 생성해보기

> **REF**  
> [기본 사용법](https://jekyllrb-ko.github.io/docs/usage/)  
> [GitHub Pages 블로그 준비하기](https://devinlife.com/howto%20github%20pages/github-prepare/)  
> [Jekyll theme을 사용하여 블로그 생성하기](https://devinlife.com/howto%20github%20pages/new-blog-from-template/)

### 새 블로그 생성

```
$ jekyll new blog
Running bundle install in /Users/minky/Documents/blog... 
  Bundler: Fetching gem metadata from https://rubygems.org/...........
  Bundler: Fetching gem metadata from https://rubygems.org/.
  Bundler: Resolving dependencies...
  ...
  Bundler: Bundle complete! 6 Gemfile dependencies, 30 gems now installed.
  Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
New jekyll site installed in /Users/minky/Documents/blog. 
```

### 서버 구동

1.  서버 실행

```
$ cd blog/
$ bundle exec jekyll serve
Configuration file: /Users/minky/Documents/blog/_config.yml
            Source: /Users/minky/Documents/blog
       Destination: /Users/minky/Documents/blog/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
       Jekyll Feed: Generating feed for posts
                    done in 0.435 seconds.
 Auto-regeneration: enabled for '/Users/minky/Documents/blog'
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.
[2020-01-30 16:32:07] ERROR `/favicon.ico' not found.
```

2.  접속 및 확인  
    출력되는 Server address로 접속해서 확인
![Install]({{path}}/img04.png){:.border width='600px'}  
*Command Line Tools Version 확인*

### 서버 호스팅

특정 IP로 서버를 호스팅해서 외부에서 접속 가능

```
$ bundle exec jekyll serve -H 192.168.0.8
```
