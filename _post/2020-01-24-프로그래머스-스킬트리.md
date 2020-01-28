# 스킬 트리

## 문제 설명
- 선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.
- 예를 들어 선행 스킬 순서가 `스파크 → 라이트닝 볼트 → 썬더`일때, `썬더`를 배우려면 먼저 `라이트닝 볼트`를 배워야 하고, `라이트닝 볼트`를 배우려면 먼저 `스파크`를 배워야 합니다.
- 위 순서에 없는 다른 스킬(`힐링` 등)은 순서에 상관없이 배울 수 있습니다. 따라서 `스파크 → 힐링 → 라이트닝 볼트 → 썬더`와 같은 스킬트리는 가능하지만, `썬더 → 스파크`나 `라이트닝 볼트 → 스파크 → 힐링 → 썬더`와 같은 스킬트리는 불가능합니다.
- 선행 스킬 순서 `skill`과 유저들이 만든 스킬트리를 담은 배열 `skill_trees`가 매개변수로 주어질 때, 가능한 스킬트리 개수를 반환 하는 `solution` 함수를 작성해주세요.

## 제한 조건
- 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
- 스킬 순서와 스킬트리는 문자열로 표기합니다.
- 예를 들어, `C → B → D` 라면 `CBD`로 표기합니다
- 선행 스킬 순서 `skill`의 길이는 `1` 이상 `26` 이하이며, 스킬은 중복해 주어지지 않습니다.
- `skill_trees`는 길이 `1` 이상 `20` 이하인 배열입니다.
- `skill_trees`의 원소는 스킬을 나타내는 문자열입니다.
- `skill_trees`의 원소는 길이가 `2` 이상 `26` 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

## 입출력 예
|`skill`|`skill_trees`|`return`|
|---|---|---|
|`"CBD"`|`["BACDE", "CBADF", "AECB", "BDA"]`|`2`|

## 내 풀이
```python
def squeeze(skills, skill_tree):
    return ''.join([_skill for _skill in skill_tree if _skill in skills])


def generate(skills):
    generated_skill_tree = []

    for length in range(1, len(skills) + 1):
        generated_skill_tree.append(skills[0:length])
    generated_skill_tree.append('')
    return generated_skill_tree


def solution(skills, skill_trees):
    squeeze_trees = [squeeze(skills, skill_tree) for skill_tree in skill_trees]
    possible = generate(skills)
    return len([squeeze_tree for squeeze_tree in squeeze_trees if squeeze_tree in possible])
```

## 해설
- 예를 들어 정해진 스킬 트리가 `"ABCDE"`라고 할 때, 가능한 스킬 찍는 방법을 모두 나열해보면 아래의 6개 상황이다.
    1. `""`
    2. `"A"`
    3. `"AB"`
    4. `"ABC"`
    5. `"ABCD"`
    6. `"ABCDE"`
- 위의 순서대로 사이사이에 반드시 순서대로 찍지 않아도 되는 스킬들이 들어간다. 이런 스킬들을 소문자로 표현하면, 예를 들면 아래와 같다.
    1. `"abAcBdeC"`
    2. `"Aabc"`
    3. `"abc"`


- 주의 해야 할 점은 __순서대로 찍어야 하는 대문자 스킬들을 하나도 안 찍어도 문제 조건에는 위배되지 않는다는 것__이다. (바로 위의 3번 예시)
- 나는 먼저 `squeeze` 함수를 통해서 굳이 순서대로 찍지 않아도 되는 스킬들을 모두 없애버린 후, `squeeze_trees`에 저장하였다. 예를 들어, `squeeze("abAcBdeC")`의 반환값은 `"ABC"`이다.
- 그리고 `generate` 함수를 통해서 해당 순서로 찍을 수 있는 모든 스킬들을 리스트로 반환하여 `possible`에 저장하였다. 예를 들어, `generate("ABC")`의 값은 `["", "A", "B", "C", "AB", "ABC"]`이다.
- 그 후에는 단순히 `squeeze_trees`의 각 원소들이 `possible`에 들어있는가 아닌가 `in`으로 판단하여 그 수를 세기만 하면 되었다.

## 새로 알게된 것

- `range()` 내장 함수를 거꾸로 사용하려면 반드시 `step` 을 음수로 설정해야 한다. 예를 들어 `10` 부터 `1` 까지 발생하는 레인지를 설정하려면 `range(10, 0)` 이 아니라 `range(10, 0, -1)` 이어야 한다.