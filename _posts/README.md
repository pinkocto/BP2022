⚠️ Do not delete this directory!  You can delete the blog post files in this directory, but you should still keep this directory around as Jekyll expects this folder to exist.

# Auto-convert markdown files To Posts

[`fastpages`](https://github.com/fastai/fastpages) will automatically convert markdown files saved into this directory as blog posts!

You must save your notebook with the naming convention `YYYY-MM-DD-*.md`.  Examples of valid filenames are:

```shell
2020-01-28-My-First-Post.md
2012-09-12-how-to-write-a-blog.md
```

# Resources

- [Jekyll posts](https://jekyllrb.com/docs/posts/)
- [Example markdown post](https://github.com/fastai/fastpages/blob/master/_posts/2020-01-14-test-markdown-post.md)

# no-display My Blog.. Solution

_notebooks에 올린 내용이 블로그에 업데이트가 안되는 경우가 종종 있다.ㅠㅠ
어떤 문제인지 찾기도 매우 힘들고 시간도 오래걸리는 문제점이 있다.

나의 경우는 보통 경로가 잘못되었거나, 데이터/그림 파일이 안올라간 경우가 제일 많았고,
정말 다 맞는것 같은데 블로그에 안보이는 경우도 더러 있었다. (그림이 포함된 주피터노트북의 경우)

그럴때는 그냥 _post에 jupyternotebook을 .md형태로 다운받아 올리는 것이 제일 간편하다.
하지만 올릴때 경로를 반드시 수정해야 그림이 눈에 보이게 된다.

다음은 예시코드이며, 파일명과 경로정도만 바꿔서 사용하면 된다.
나는 저장소의 images파일에 사진을 저장해놓았다. 따옴표 안의 문구는 사진에 대한 주석이다.

`![]({{ site.baseurl }}/images/dist.PNG "두 군집 사이의 유사성/거리 측정")`


