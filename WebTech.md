= Web Technologies : Reminders and Trainers
Jonggun Gim <jonggun.gim@gmail.com>
:description: This document is for amassing information about fundamental web technologies
:author: Jonggun Gim
:sectnums:
:toc: left
:doctype: manpage
:source-highlighter: highlight.js

== About this document
{description}

.Revisions
[format="csv", options="header"]
|===
Date, Description
2020/12/02,Transplanted from Notion.
2020/12/04, Drafted with a template.
2020/12/04, Moved Angular GAE pages to this.
|===


== HTML5
.Basic HTML
[source,html,%collapsible]
----
<HTML></HTML>
<head></head>
<body></body>
<title></title>
<H1></H1> 123456
<p></p> : paragraph
<br>: 다음 줄로 넘어감
<!— comment —>
<style></style>
----
.Formatting
[source,html]
----
<del></del>
----
.audio/video
[source,html]
----
<img src="a.jpg" width="300" height="200">
<audio>
<video>
<source>
----
.Links
[source,HTML]
----
 <a href="">이름 </a>
 <nav></nav>
----
.Lists
[source,HTML]
----
<ul><ol><dl>
   <li></li>
</ul></ol></dl>
----
.Table
[source,html]
----
<table>
   <tr>
       <th>이름</th> <th>성적</th>
   <tr>
       <td>uneji</td><td>100</td>
       <td>jonggun</td><td>70</td>
   <tr>
<table>
----

.Form
[source,html]
----
<form>
   <label>name: </label> <input type="text"><br>
   <button>눌러</button>
</form>
----

== CSS
[source, html]
----
body{
	background-color: lightblue;
}
h1{
	color: yellow;
	text-align: center;
	font-size: 20px;
	font-family: verdana;
}
----

[source, html]
----
<html>
    <head>
        <style>
            .box, #m_box{width:100px;height: 50px; border:1px solid green}
            #m_box {background-color:yellow}
        </style>

    </head>
    <body>
        <div class="box">box class</div>
        <div id="m_box">m_box</div>
    </body>
</html>
----

div : block을 수직으로 쌓는 구조, span: block을 수평으로 쌓는 구조

* id:  CSS selector # (sharp)
* class: CSS selector . (dot)

== JavaScript
https://github.com/getify/You-Dont-Know-JS[getify/You-Dont-Know-JS]

```html
<html>
    <script>
        function say(m){
            alert(m)
        }
    </script>

<head>
    <title>Learn Web for G</title>
</head>
<a href="scratch.html">Vue JS</a>
<br>
<form>
    <label>name: </label><input name="message" type="text"><button onclick="say(name.value)">go</button>
</form>
</html>
```

.let, var
.alert, prompt
.console.log
[source,JavaScript]
----
let theNumber = Number(prompt("Pick a number")); if (!Number.isNaN(theNumber)) {
console.log("Your number is the square root of " + theNumber * theNumber);
}
----    
.if
.for
.comments
.function
[source,JavaScript]
----
    const square1 = function(x) {
       return x * x;
    };
    function square2(x) {
       return x * x;
    }
    const square3 = (x) => {
       return x*x;
     };
----

.array
[source,JavaScript]
----
let sequence = [1, 2, 3]; sequence.push(4); sequence.push(5); console.log(sequence);
// → [1, 2, 3, 4, 5]
for(let a of sequence){
   console.log(a);
}
----    

=== DOM (Document Object Model)
.finding elements
[source,JavaScript]
----
let link = document.body.getElementsByTagName("a")[0]; console.log(link.href);
document.getElementById("gertrude");
----

.adding elements
[source,JavaScript]
----
<p>One</p>
<p>Two</p>
<p>Three</p>

<script>
let paragraphs = document.body.getElementsByTagName("p"); document.body.insertBefore(paragraphs[2], paragraphs[0]);
</script>

<p>The <img src="img/cat.png" alt="Cat"> in the <img src="img/hat.png" alt="Hat">.</p>
<p><button onclick="replaceImages()">Replace</button></p>
<script>
function replaceImages() {
let images = document.body.getElementsByTagName("img"); for (let i = images.length - 1; i >= 0; i--) {
let image = images[i]; if (image.alt) {
let text = document.createTextNode(image.alt);
image.parentNode.replaceChild(text, image); }
} }
</script>
----

.Handling Events
[source,JavaScript]
----
<button>Click me</button> <p>No handler here.</p> <script>
let button = document.querySelector("button"); button.addEventListener("click", () => {
console.log("Button clicked."); });
</script>
----

== Angular
https://www.javatpoint.com/angular-7-installation[Angular 7 Installation - Javatpoint]

http://www.codaffection.com/angular-article/angular-7-crud-with-firestore/[Angular 7 CRUD with Firestore]

.work flow
[source,shell]
----
ng new [name]
npm install firebase @angular/fire
vim src/environment/environment.ts
vim src/app/app.module.ts

ng serve --o
ng generate component empoloyees
ng g c employees/employee
ng g service shared/employee
[for model]
ng g class shared/employee --type=model
----

== Vue
=== Crash Course
* Merge of MVC
* Vue-cli 3
* Npm install -g install @vue/cli
* Vue create name
* Npm run server. In that directory
* <div id="app></div>
* Vue ui --- project manaager
* Index.html
* Main.js
* App.vue
[source, html]
----
<template>
    <div id ="app>. Only one <div> allowed in the template
        <todos v-bind>
<script>
    Export default {name, component
    data returns todos
    Can be implemented in anew file todos.vue
<style scoped>
----
* Todos.vue
** <div v-bind="todos" v-for "todo in todos">
* TodoItem.vue

=== Key Points
* [x]  new Vue({el:, data: }); (500505)
* [x]  v-if (500505)
* [x]  {{}} (500505)
* [x]  v-for (500505)
* [x]  v-bind, <button :disabled="buttonDisabled"> (500505)
* [x]  v-model (500505)
* [ ]  method
* [ ]  this
* [ ]  computed
* [ ]  watchers , deep watching
* [ ]  filters
* [ ]  ref
* [ ]  inputs and events. v-on
* [ ]  Event Modifiers
* [ ]  beforeCreate, created, beforeMount, mounted, beforeUpdate, updated, beforeDestroy, destroyed
* [ ]  custom directives
* [ ]  hook arguments
* [ ]  CSS transitions
* [ ]  JavaScript Animations
* [ ]  Component Basics
* [ ]  Passing in Data
* [ ]  props:
* [ ]  .sync
* [ ]  Slots
* [ ]  Custom Events
* [ ]  Mixins
* [ ]  vue-loader and .vue
* [ ]  Class Binding for styling with Vue
* [ ]  scoped CSS with vue-loader
* [ ]  preprocessor
* [ ]  render()
* [ ]  client-side routing with vue-router
* [ ]  Navigation Guards
* [ ]  Vuex (State Management)
* [ ]  boot strapping with vue-cli

=== Deployment
==== To GitHub
1. vue.config.js 
[source, json]
module.exports = {
	publicPath: '/reponame/'
}

1. on terminal
[source, bash]
git checkout --orphan gh-pages
npm run build
git --work-tree dist add -all
git --work-tree dist commit -m 'deploy'
git push origin HEAD:gh-pages --force
rm -r dist
git checkout -f master
git branch -D gh-pages

1. select 'gh-pages' from Setting>Github Pages

=== Links
. https://vuejs.org/v2/guide/[Introduction - Vue.js]
. https://riptutorial.com/Download/vue-js.pdf
. https://codesandbox.io/embed/runtime-http-ebup4?codemirror=1[namecards]
. https://blog.logrocket.com/how-to-build-and-deploy-a-vue-js-crud-app-with-cloud-firestore-and-firebase/[How to build and deploy a Vue.js CRUD app with Cloud Firestore and Firebase - LogRocket Blog]
. https://vuejsexamples.com/20-best-landing-page-template-with-vuejs/[20 Best Landing Pages Template With Vuejs]
. https://www.taniarascia.com/getting-started-with-vue/[Vue Tutorial: An Overview and Walkthrough]
. https://nykim.work/73?category=785004[[Vue] 기초 스터디]
. https://nykim.work/74?category=785004[ 뷰 실습 - Todo 웹앱 만들기 (1)]
. https://www.linode.com/docs/development/javascript/how-to-build-and-use-vuejs-components/[Building and Using VueJS Components - A Tutorial]





== Firebase Hosting
https://firebase.google.com/?hl=ko[Firebase]

https://medium.com/google-developers/whats-the-relationship-between-firebase-and-google-cloud-57e268a7ff6f[What's the relationship between Firebase and Google Cloud?]

=== setting
https://console.firebase.google.com/project/inventoryg-218113/hosting[Sign in - Google Accounts]

.Firebase CLI
[source,shell]
----
brew update
brew install node
npm install -g firebase-tools
----

.Vue CLI/Firebase Project Init/Deploy
[source,shell]
----
sudo npm install -g @vue/cli
vue create [name]
firebase login
firebase init
npm run build
firebase deploy
----

IMPORTANT: node_modules 삭제한 다음 관리하고.. 다시 빌드할 경우에는 node install 명령어로 복구 가능

IMPORTANT: DropBox에서 node_modules를 계속 싱크하려면 시간이 너무 많이 걸리므로 DropBox 내에 git을 다른 폴더로 clone 한 다음에 이를 push 하면 될 것 같음.

== Google AppEngine
https://console.cloud.google.com/appengine?project=egtutor-hrd&serviceId=default&duration=PT1H[Google Cloud Platform]

https://cloud.google.com/certification?hl=ko[Google Cloud Certifications]

=== App Engine New Application with Python
* app.yaml
* main.py
```python
from flask import Flask
app = Flask(__**name__**)
@app.route('/')
def hello():
	return 'Hello'
```
* requurements.tx
[source, shell]
----
gcloud projects create [id]
gcloud projects describe [id]
gcloud app create --project=[id]
gcloud projects list
gcloud config set project [id]
gcloud app deploy
gcloud app browse
----
