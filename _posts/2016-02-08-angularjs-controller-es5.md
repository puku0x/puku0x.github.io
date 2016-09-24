---
layout: post
title: モダンなAngularJSの書き方（コントローラ）
subtitle: Modern AngularJS
---

備忘録を兼ねて、現在調べている範囲で書きます。

- 基本的にstrictモードで書く
- $scopeは使わない
- コンポーネント化を意識する

の３点に気をつけて書くとこうなります。


```javascript
(function(){
    'use strict';
	
    // モジュール定義
    angular
		.module('app', ['ngMaterial'])
		.controller('MainController', controller);
	
	// コントローラ
	function controller($mdSidenav) {
		var self = this;
		
        // ナビゲーションドロワー切り替え
        function toggleSideNav() {
            $mdSidenav('left').toggle();
        }
	}
})();
```

function(){}で囲む必要は特にないです。thisをコントローラ内の変数に代入している理由は後ほど明らかになります。

$scopeやら無名関数やらが消えてソースが見やすくなりましたね。

HTML内で使う場合はController asで

```html
<body ng-app="app" ng-controller="MainController as main" layout="row" ng-cloak >
	<md-sidenav class="site-sidenav md-sidenav-left md-whiteframe-z2" md-component-id="left" ng-click="main.toggleSideNav()" md-is-locked-open="$mdMedia('gt-sm')">
        <md-toolbar class="md-whiteframe-z1">
```

こんな感じに別名を付け、メンバへのアクセスは「別名.メンバ名」のようにします。

ES6でない時点で「モダン」ではありませんが、まだ勉強中の身ですのでご了承ください。
