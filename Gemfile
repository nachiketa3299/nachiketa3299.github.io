# frozen_string_literal: true


git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }

# gem "rails"

# 나는 프로젝트 의존요소 목록인 Gemfile을 생성하기 위해 bundle init 명령어를 사용하였다.
# Gemfile은 사이트에 필요한 젬들의 목록입니다.

source "https://rubygems.org"
gem "jekyll" # Gemfile에 jekyll을 의존요소로 추가하는 것.

# 이제부터 언급된 모든 Jekyll 명령어 앞에 bundle exec를 붙여 실행하면 항상 Gemfile에 정의된 버전의 Jekyll을 사용할 수 있다.
# 터미널에 bundle install치면 Gemfile.lock을 생성하는데, 현재 버전의 젬파일들로 잠금한다.젬버전을 업데이트하고 싶으면 bundle update를 사용하면 된다.
# 젬파일을 사용할 때에는 bundle exec jekyll serve라는 명령어를 사용한다. 이것은 오직 너의 Gemfile에만 존재하는 루비 환경을 사용하도록 강제한다.

group :jekyll_plugins do
    gem 'jekyll-sitemap'
    # 검색엔진이 내용물을 인덱싱 할 수 있는 사이트맵을 만든다.
    gem 'jekyll-seo-tag'
    # 너의 포스트를 위한 RSS 피드를 만든다.
    gem 'jekyll-feed'
    # SEO를 돕기 위한 메타 태그를 추가한다.
end
# 여기서만 추가하는 것이 아니라, _config.yml도 수정해야함.
