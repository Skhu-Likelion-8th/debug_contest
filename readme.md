## !! 2020 멋쟁이 사자처럼 디버깅 콘테스트 답지 !!

#### 로그인
```python
# views.py > 99, 100
# 정답
username = request.POST['username']
password = request.POST['password']

# 오답
username = request.post['username']
password = request.post['password']
```

#### 로그인 실패 시
```python
# views.py > 107
# 정답
else:
    return HttpResponse("로그인 실패. 다시 시도해보세요 ㅋ")

# 오답
else:
    return render(HttpResponse("로그인 실패. 다시 시도해보세요 ㅋ"))
```

#### 회원가입
```python
# views.py > 111, 112
# 정답
form = UserForm(request.POST)
        if form.is_valid():

# 오답
f = UserForm(request.POST)
        if form.is_valid():
```
- 위를 form으로 혹은 아래를 f로 바꾸면 됨

#### 로그아웃
```python
# urls.py > 35
# 정답
path('', include('django.contrib.auth.urls')),

# 오답
path('', include('django.contrib.auth.url')),
```

#### 로그인 안하고 글 작성
```python
# views.py > 18, 19
# 정답
if not request.user.is_active:
        return HttpResponse("Can't wirte a post without Sign In")

# 오답
if request.user.is_active:
        return HttpResponse("Can't wirte a post without Sign In")
```

#### 글 작성
```python
# views.py > 27
# 정답
hashtag_field = form.cleaned_data['hashtag_field']

# 오답
hashtag_field = form.cleaned_data['hashtag_fields']
```
- `forms.py`를 수정해도 인정

#### 글 수정
```python
# views.py > 54
# 정답
post = get_object_or_404(Post, pk=pk)

# 오답
post = get_object_or_404(Post, pk)
```

#### 글 삭제
```python
# views.py > 79
# 정답
post.delete()

# 오답
post.remove() #이거되나근데..?
```

#### 글 수정, 삭제 시 작성자와 비교
```python
# views.py > 58, 76
# 정답
elif post.writer != request.user:
    return HttpResponse("자기가 쓴 글만 삭제할 수 있어용")

# 오답
elif post.writer == request.user:
    return HttpResponse("자기가 쓴 글만 삭제할 수 있어용")
```


#### 댓글 작성
```python
# views.py > 86, 92
# 정답
post = get_object_or_404(Post, id=post_id)
...
comment.post_id = post

# 오답
article = get_object_or_404(Post, id=post_id)
...
comment.post_id = post
```
- 둘 중 하나 수정하면 ㅇㅋ

#### 해시태그별 보기
```django
 <!-- hashtag.html > 20 -->
<!-- 정답 -->
{% for post in hashtag.post_set.all %}

<!-- 오답 -->
{% for post in hashtag.posts.all %}
```
- `models.py`에서 `related_name` 수정해도 ㅇㅈ

#### 좋아요
```django
<!-- main.html > 70 -->
<!-- 정답 -->
<a href="{% url 'like' pk=post.pk %}">

<!-- 오답 -->
<a href="{% url 'like' name=post.pk %}">
```
- html 파일 외에 urls, views를 `name`으로 설정해도 ㅇㅈ