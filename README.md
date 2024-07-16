# takoyaki65.github.io

### Webrickが初期段階でインストールされていない問題。
これにより、ローカルでビルドを行う際にエラーが発生してしまう。

二番目のアンサーを参照

ref: https://stackoverflow.com/questions/75912209/build-error-while-trying-to-publish-my-github-pages

> My jekyll theme also gets this warning, and the answer provided by @BenjaminW. helped me find the solution.
>
>As he said, this warning simply tells you that the local Gemfile contains a dependency that isn't supported by GitHub Pages. There is a bit of a catch-22 with my case, and I suspect many others as well:
>
>Previously, the webrick library came pre-installed with Ruby. This is needed when building jekyll locally. In Ruby 3.0, they removed webrick, so now you must explicitly add webrick to your Gemfile if you want to build a jekyll site locally (GitHub also mentions this issue). The problem is that webrick is not one of the gems that are supported by GitHub Pages. Therefore, when GitHub Pages builds a site and it sees webrick, it gives you that warning message, just to let you know that you're using a dependency that GitHub Pages doesn't support.
>
>If your case is similar to mine, it's fine to ignore. It happens because I want to be able to build my site locally AND using GitHub Pages. When I build locally, I need webrick, and when it gets build with GitHub Pages it works just fine, but it just gives you that warning. In my case, if I remove the Gemfile or the webrick line within it, the warning goes away. But then I can't build locally, so I just leave it and live with the warning.

Gemfileに、github-actionsの環境でない場合のみwebrickを追加することで解決した。
参考: https://github.com/github/pages-gem/issues/887#issuecomment-1773067676
```
install_if -> { ENV["GITHUB_ACTIONS"] != "true" } do
  puts "Is GitHub action: #{ENV["GITHUB_ACTIONS"] == "true"}"
  gem "webrick", "~> 1.8"
end
```
