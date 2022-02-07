---
title: coding self training
author: ''
date: '2022-02-07'
slug: []
categories: []
tags:
  - python
  - coding
  - algorithm
  - programmers.co.kr
Description: ''
Tags: []
Categories: []
DisableComments: no
---

Recently, I am training myself on coding. because it's been long time since I became data engineer. I began to make some plans this year, and one of them is coding ability. 

what coding language? I was interested in lisp like program such as common lisp, clojure. These kind of languages are good at self thought improvement(?), but actually it's not good at coding interview problems. Yes, I admit that I am not enough to get through them.Anyway, I decided it with python3. ;) 

I am solving one by one and step by step on coding site problems. I completed level 1 and entered level 2. :) but when I almost ending up them, I faced a hard one. :( Wow, I don't know it's coding issue. To me, it is interpretation issue. I could understand what the problem is saying at all. 

the problem is 
https://programmers.co.kr/learn/courses/30/lessons/86052

my solution is very spaghetti like. but I am happy anyway I solved it myself. L0L 


```python 
def solution(grid):
    answer = []
  
    m = len(grid)
    n = len(grid[0])
    isvisit = {}
    
    from_src = {(0,1) : 'L',
                (1,0) : 'U',
                (-1,0): 'D',
                (0,-1): 'R'}
    
    to_target = {'R': {'L': (1,0), 'U':(0,-1), 'R':(-1,0), 'D':(0,1)},
                'L': {'L': (-1,0), 'U':(0,1), 'R':(1,0), 'D':(0,-1)},
                'S': {'L': (0,1), 'U':(1,0), 'R':(0,-1), 'D':(-1,0)}}
    curs = []
    for i in range(m):
        for j in range(n):
            curs.append((i,j))
    
    #cur = (0,0) #(0,0)
    for cur in curs:
        
        for d in [(1,0),(0,1),(-1,0),(0,-1)]:
            tmp_to = from_src[d]
            to = ((cur[0]+d[0])%m, (cur[1]+d[1])%n)
            cnt = 0

            while isvisit.get(str(cur)+from_src[d]+"::"+str(to)+grid[to[0]][to[1]], 0) == 0:
                cnt += 1
                isvisit[str(cur)+from_src[d]+"::"+str(to)+grid[to[0]][to[1]]] = 1            
                val = grid[to[0]][to[1]]
                tmp_next = to_target[val][from_src[d]]
                cur = to
                to = (to[0] + tmp_next[0])%m, (to[1] + tmp_next[1])%n
                d = to_target[val][from_src[d]]            


            if cnt > 0 :
                answer.append(cnt)
            
    
    return sorted(answer)
```


long story to short, I think this is very good experience and good stimulus. I found that I forgot many basic grammars and tricks. I need to remind of all kinds of them. 


