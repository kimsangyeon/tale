---
layout: post
title: "Django Widget"
author: "Yeon"
---

# Django Widget

## Widget 정의
- 위젯은 Django가 HTML 입력 요소를 표현한 것입니다. 위젯은 HTML 렌더링을 처리하고 위젯에 해당하는 GET/POST에서 데이터를 추출합니다.

### Form
- 장고의 Feature중 하나
- 일반폼 일 경우 직접 필드 정의 위젯 설정 필요
- 모델폼 일 경우 모델과 필드를 지정하면 모델폼이 자동으로 폼 필드를 생성

#### 위젯 지정
```python
from django import forms

class CommentForm(forms.Form):
    name = forms.CharField()
    url = forms.URLField()
    comment = forms.CharField(widget=forms.Textarea)
```
Textarea 사용시 기본 위젯 TextInput에서 변경됩니다


##### 필드에서 위젯 정의 및 인수 설정
```python
from django import forms

BIRTH_YEAR_CHOICES = ('1980', '1981', '1982')
FAVORITE_COLORS_CHOICES = (
    ('blue', 'Blue'),
    ('green', 'Green'),
    ('black', 'Black'),
)

class SimpleForm(forms.Form):
    birth_year = forms.DateField(widget=forms.SelectDateWidget(years=BIRTH_YEAR_CHOICES))
    favorite_colors = forms.MultipleChoiceField(
        required=False,
        widget=forms.CheckboxSelectMultiple,
        choices=FAVORITE_COLORS_CHOICES,
    )
```
위젯을 정의하며 각 위젯에 맞게 인수 설정가

##### 위젯 사용자 정의 스타일
```python
class CommentForm(forms.Form):
    name = forms.CharField(widget=forms.TextInput(attrs={'class': 'special'}))
    url = forms.URLField()
    comment = forms.CharField(widget=forms.TextInput(attrs={'size': '40'}))

### or update 사용
###
class CommentForm(forms.Form):
    name = forms.CharField()
    url = forms.URLField()
    comment = forms.CharField()

    name.widget.attrs.update({'class': 'special'})
    comment.widget.attrs.update(size='40')

### or 모델 필드가 없는 경우 Forms.fields 속성 사용
###
class CommentForm(forms.ModelForm):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.fields['name'].widget.attrs.update({'class': 'special'})
        self.fields['comment'].widget.attrs.update(size='40')

```
###### 스타일 적용된 위젯 랜더링
```HTML
>>> f = CommentForm(auto_id=False)
>>> f.as_table()
<tr><th>Name:</th><td><input type="text" name="name" class="special" required /></td></tr>
<tr><th>Url:</th><td><input type="url" name="url" required /></td></tr>
<tr><th>Comment:</th><td><input type="text" name="comment" size="40" required /></td></tr>
```



[참고: Django Widget](https://docs.djangoproject.com/en/2.0/ref/forms/widgets/)