#### init_clone.svg image @ <a href="https://bramp.github.io/js-sequence-diagrams/">JS sequence diagram</a>
```
participant git.openstack.org/openstack/project as A
participant review.intra.alchelabo.com as B
participant git.alchelabo.com as C

note over C: manual\n creation of \nthe project
note over B: rm -rf repository-directory/*
A-->B: git clone --mirror git.openstack.org/openstack/project
B-->C: sync Read/Only
```


#### update_review_file.svg image @ <a href="https://bramp.github.io/js-sequence-diagrams/">JS sequence diagram</a>
```
participant local machine as A
participant gerrit/openstack/kolla as B
participant gitlab/openstack/kolla as C

note over C: manual creation\n of the project
B-->>A: git clone ssh://user@host:port
A-->A: git checkout -b <branch name> <tag>
A-->A: fix .gitreview file
A-->A: git commit -am "commit message"
A-->B: git push --set-upstream origin <branch name>
B-->C: sync Read/Only
```


#### feature_branch_flowchart.png @ <a href="http://flowchart.js.org/">Flowchart</a>
(To export this image, I've used the screeshot feature enabled in Firefox)

```flow
st=>start: git checkout -b feature/xyz
e=>end
cond1=>condition: fresh clone?
sub1=>subroutine: git review -s
op2=>operation: ...coding...
op3=>operation: Run test suit
op4=>operation: git merge feature/xyz trustack/stable_branch
cond2=>condition: Test passed ?
io=>operation: git commit -am 'commit message'

st->cond1
cond1(no)->op2
cond1(yes)->sub1
sub1(right)->op2
op2->op3->cond2
cond2(yes)->io->op4->e
cond2(no)->op3
```
