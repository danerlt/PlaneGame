#**PlaneGame设计说明书**

---

[TOC]

---
##1 引言  
###1.1 编写目的 
  随着科技的发展，现在电脑的功能已不仅仅是简单的上网、收发邮件了。更多的电脑用户希望在工作、学习之余通过方便灵巧可随身携带的仪器休闲娱乐。因此，为了迎合众多用户的需求并适应现在电脑的规模，我们开发出一套适合各阶层人士的具有很强的娱乐性和交互性的雷霆战机游戏。 
  雷霆战机,之所以取这样的名字，去用意还是很明显的.雷霆战机其实就是一个英雄的化身，它是人不断向前追求和勇气的象征.就像现代的人只有不断努力向前争取和勇于战胜困难才能得到自己想要的。而敌机也是随机出现的，就像现在社会存在的机会，而我们只有找好自己的目标才能成功。 
    虽然现在市面上存在着各种各样的游戏版本,可是雷霆战机其市场还是相当大的。因为它的特殊在于它能吸引人更深入，爱不释手.随着游戏速度不断加快，其刺激性也更强。可以说该游戏的优势在于它的简单易行，不论是电脑，还是小游戏机，都能很快顺利的运行。对于在外忙碌的人，不可能花费大量时间在娱乐上，大型游戏是行不通的。这样的小游戏刚好迎合了他们的需求。
###1.2 背景  
  随着科技的发展，现在电脑的功能已不仅仅是简单的上网、收发邮件了。更多的电脑用户希望在工作、学习之余通过方便灵巧可随身携带的仪器休闲娱乐。因此，为了迎合众多用户的需求并适应现在电脑的规模，我们开发出一套适合各阶层人士的具有很强的娱乐性和交互性的雷霆战机游戏。 
  雷霆战机,之所以取这样的名字，去用意还是很明显的.雷霆战机其实就是一个英雄的化身，它是人不断向前追求和勇气的象征.就像现代的人只有不断努力向前争取和勇于战胜困难才能得到自己想要的。而敌机也是随机出现的，就像现在社会存在的机会，而我们只有找好自己的目标才能成功。 
    虽然现在市面上存在着各种各样的游戏版本,可是雷霆战机其市场还是相当大的。因为它的特殊在于它能吸引人更深入，爱不释手.随着游戏速度不断加快，其刺激性也更强。可以说该游戏的优势在于它的简单易行，不论是电脑，还是小游戏机，都能很快顺利的运行。对于在外忙碌的人，不可能花费大量时间在娱乐上，大型游戏是行不通的。这样的小游戏刚好迎合了他们的需求。   
###1.3 定义  
  需求：用户解决问题或达到目标所需的条件或功能；系统或系统部件要满足合同、标准，规范或其它正式规定文档所需具有的条件或权能。而且其很强的交互性及简单易行性，可以让人在很短时间内熟悉它的游戏规则，不论用户文化水平如何，都会很轻松的学会使用它。 
  
---
###1.4参考资料  
[张海藩](http://www.baike.com/wiki/%E5%BC%A0%E6%B5%B7%E8%97%A9)：《软件工程导论》清华大学出版社 2008年2月第五版  
[肖刚](http://baike.baidu.com/link?url=fYHyxA88Es5FsyR71Pw9fiVGLAFuuF4pYcLvvkNbIlBcVFSXgU45Dty1DgtD4CfSzrhfRUjMrdqoZ_5I8ynWZ_ifqrGIGSW6w3XkFPU16fTjgi6E52i7w9bGPAgGzk_ZZ3vDH_qZGwu7zL5ON-jM16PES1poFIB14g-TkFGsOfS)：   《实用软件文档写作》清华大学出版社 2005年2月

---
##2 程序系统总体设计

| 模块名称     | 功能简述 | 
 | --------   | :-----:  | 
| 人机智能       |   人机对战规则的实现   |     
| 游戏对象        |    各个游戏对象的抽象父类    |
| 战机对象        |    战机类    |
| 爆炸对象        |    爆炸类    |
| 文字对象        |    文字类    |

##3 程序设计说明
###3.1 程序重要代码描述
```python
<div class="showSomething">
			<div id="booms">爆炸使用情况(已使用/存储总量)：</div>
			<div id="missle">子弹使用情况(已使用/存储总量)：</div>
		</div>
		<script src="js/data.js"></script>
		<script src="js/loading.js"></script>
		<script src="js/allSprite.js"></script>
		<script>
			var canvas = document.getElementById("cas");
			canvas.height = window.innerHeight;
			var ctx = canvas.getContext('2d');

			var img = new Image(),
				boomDom = document.getElementById("booms"),
				missleDom = document.getElementById("missle"),
				menu = document.getElementById("menu"), //获取主菜单
				start = document.getElementById("start"),//获取开始游戏
			setting = document.getElementById("setting"), //获取设置
				help = document.getElementById("help"), //获取帮助
				about = document.getElementById("about"), //获取关于
				back = document.getElementById("back"),//获取返回
				
menu_setting=document.getElementById("menu_setting"),//获取设置菜单
menu_lever = document.getElementById("menu_lever"),//获取难度等级选择菜单
menu_music = document.getElementById("menu_music");//获取声音设置菜单
			    
			    
			  var globalID ;
			  //获取
			  requestAnimationFrame
			window.RAF = (function() {
				return window.requestAnimationFrame || window.webkitRequestAnimationFrame || window.mozRequestAnimationFrame || window.oRequestAnimationFrame || window.msRequestAnimationFrame || function(callback) {
					window.setTimeout(callback, 1000 / 60);
				};
			})();

			//      var CAF = (function(){
			//      	return window.cancelAnimationFrame ||window.webkitCancelAnimationFrame || window.mozCancelAnimationFrame || widow.oCancelRequestAnimationFrame || window.msCancelRequestAnimationFrame ;
			//      })();	

			Array.prototype.foreach = function(callback) {
				for(var i = 0; i < this.length; i++) {
					callback.apply(this[i], [i]);
				}
			}

			var sprites = [], //精灵表
				missles = [], //子弹
				booms = [], //爆炸
				badPlanNum = 30, //敌机数量
				point = 0,
				myplan = null, //我方飞机
				eatfood = null, //道具
				foodDate = null, //道具产生时间
				dieNum = 0; //死亡次数
            bgmisplay = true;//背景音乐 为true时播放，为false时不播放
			//按下键盘时将myplan对应的属性改为true
			window.onkeydown = function(event) {
				switch(event.keyCode) {
					case 88:
						myplan.fire = true; //x键 
						break;
					case 90:
						myplan.rotateLeft = true; //Z键 向左旋转
						break;
					case 67:
						myplan.rotateRight = true; //C键 向右旋转
						break;
					case 37:
						myplan.toLeft = true; //左
						break;
					case 38:
						myplan.toTop = true; //上
						break;
					case 39:
						myplan.toRight = true; //右
						break;
					case 40:
						myplan.toBottom = true; //下
						break;
				}
			}

			//松开键盘时将
			myplan对应的属性改为false
			window.onkeyup = function(event) {
				switch(event.keyCode) {
					case 88:
						myplan.fire = false;
						break;
					case 90:
						myplan.rotateLeft = false;
						break;
					case 67:
						myplan.rotateRight = false;
						break;
					case 37:
						myplan.toLeft = false;
						break;
					case 38:
						myplan.toTop = false;
						break;
					case 39:
						myplan.toRight = false;
						break;
					case 40:
						myplan.toBottom = false;
						break;
				}
			}

			//退出
document.getElementById("quit").onclick = function closeWebPage() {
		if(navigator.userAgent.indexOf("MSIE") > 0) { //close IE  
					if(navigator.userAgent.indexOf("MSIE 6.0") > 0) {
						window.opener = null;
						window.close();
					} else {
						window.opener = null;
						window.open('', '_self');
						window.close();
					}
				} else if(navigator.userAgent.indexOf("Firefox") > 0) { //close firefox  
					window.location.href = 'about:blank ';
				} else { //close chrome;It is effective when it is only one.  
					window.opener = null;
					window.open('', '_self');
					window.close();
				}
			}
		
			//飞机爆炸            	      
			function boom(plan) {
				for(var j = 0; j < booms.length; j++) {
					if(!booms[j].visible) {
						booms[j].left = plan.left;
						booms[j].top = plan.top;
						booms[j].visible = true;

						var audio = document.getElementsByTagName("audio");
						for(var i = 0; i < audio.length; i++) {
							if(audio[i].src.indexOf("boom") >= 0 && (audio[i].paused || audio[i].ended)) {
								audio[i].play();
								break;
							}
						}
						break;
					}
				}
			}

			/**
			 *  舞台
			 *  init() 
			 *  addElement() 
			 *  myplanReborn()
			 *  update()
			 *  loop()
			 *  start()
			 */
			//var sttop;
			var stage = {
				init: function() {
					var _this = this; //解决this历史遗留问题
					this.loading = new Loading(datas, canvas, function() {
						menu.style.display = "block";
						canvas.className = "showBg"
						if(bgmisplay === true){
						    document.getElementById("bgm").play();
						}
						//点击开始按钮    隐藏菜单
						start.addEventListener("click", function() {
							menu.style.display = "none";
							back.style.display = "inline";
							_this.addElement();
						}, false);
						//点击设置信息  
						setting.addEventListener("click", function() {
						    menu_setting.style.display ="block";
						    menu.style.display ="none" ;
							//难度选择
	document.getElementById("setting_lever").onclick = function() {
								menu_setting.style.display = "none";
								menu_lever.style.display = "block";
								//简单
	one_lever.addEventListener("click",function(){
									badPlanNum = 15;
									menu_lever.style.display = "none";
									back.style.display = "inline";
									_this.addElement();
								},false);
								//一般
								two_lever.addEventListener("click",function(){
									badPlanNum = 20;
									menu_lever.style.display = "none";
									back.style.display = "inline";
									_this.addElement();
								},false);
			                    //困难
			                    three_lever.addEventListener("click",function(){
									badPlanNum = 40;
									menu_lever.style.display = "none";
									back.style.display = "inline";
									_this.addElement();
								},false);
			                    //地狱
			                     four_lever.addEventListener("click",function(){
									badPlanNum = 50;
									menu_lever.style.display = "none";
									back.style.display = "inline";
									_this.addElement();
								},false);
							}
							//背景音量设置
							document.getElementById("setting_radio").onclick = function() {
									menu.style.display = "none";
									menu_setting.style.display = "none";
									menu_music.style.display = "block";
								}
							//静音
							document.getElementById("shutdown").onclick = function() {
								    bgmisplay = false;
									document.getElementById("bgm").pause();
								}
							//正常
							document.getElementById("turn_up").onclick = function() {
								bgmisplay = true;
								document.getElementById("bgm").play();
							}

							//返回上一页_难度等级设置
							document.getElementById("lever_return").onclick = function() {
									menu_lever.style.display = "none";
									menu_music.style.display = "none";
									menu_setting.style.display = "block";
								}
							//返回上一页_背景声音设置
							document.getElementById("music_return").onclick = function() {
								menu_music.style.display = "none";
								menu_setting.style.display = "block";
							}

							//返回主菜单
							document.getElementById("setting_return").onclick = function() {
								menu_setting.style.display = "none";
								menu_music.style.display = "none";
								menu.style.display = "block";
							}

							//设置背景图
							var i = 0;
							document.getElementById("setting_bgimage").onclick = function() {
								i = i + 1;
								var imgC = document.getElementById("movebg");
								imgC.style.backgroundImage = "url(image/bg" + i + ".jpg)";
								if(i >= 3) {
									i = 0;
								}
							}
						}, false);
						//点击帮助按钮    显示帮助信息
						help.addEventListener("click", function() {
							menu.style.display = "none";
							helpDiv.style.display = "block";
							aboutDiv.style.display = "none";
							document.getElementById("help_return").onclick = function(){
								menu.style.display = "block";
								helpDiv.style.display = "none";
							};
						}, false);
						//点击关于按钮   显示关于信息
						about.addEventListener("click", function() {
							menu.style.display = "none";
							helpDiv.style.display = "none";
							aboutDiv.style.display = "block";
							document.getElementById("about_return").onclick = function(){
								menu.style.display = "block";
								aboutDiv.style.display = "none";
							};
						}, false);
						//点击退出按钮
						back.addEventListener("click", function() {
							menu.style.display = "block";
							canvas.className = "showBg"
     						back.style.display = "none";
							helpDiv.style.display = "none";
							aboutDiv.style.display = "none";
							window.open("index.html",'_self') 
						}, false);
					});

				},

				addElement: function() {
					for(var i = 0; i < 50; i++) {
						var x = Math.random() * canvas.width;
						var y = Math.random() * 2 * canvas.height - canvas.height;
						var star = new Sprite("star", starPainter, starBehavior);
						star.top = y;
						star.left = x;
						sprites.push(star);
					}

					for(var i = 0; i < badPlanNum; i++) {
						var x = Math.random() * (canvas.width - 2 * planSize().w) + planSize().w;
						var y = Math.random() * canvas.height - canvas.height;
						var badPlan = new Sprite("badPlan", badPlanPainter, badPlanBehavior);
						badPlan.top = y;
						badPlan.left = x;
						sprites.push(badPlan);
					}

					for(var i = 0; i < 400; i++) {
						var missle = new Sprite("missle", misslePainter, missleBehavior);
						missle.visible = false;
						missles.push(missle);
					}

					for(var i = 0; i < badPlanNum; i++) {
						var img = new Image();
						img.src = "image/explosion.png";
						var boom = new Sprite("boom", new SpriteSheetPainter(explosionCells, false, function() {
							this.visible = false;
						}, img));
						boom.visible = false;
						booms.push(boom);
					}

					eatfood = new Sprite("food", foodPainter, foodBehavior);
					eatfood.left = Math.random() * canvas.width - 60 + 30;
					eatfood.top = -30;
					eatfood.visible = false;
					sprites.push(eatfood);

					img.src = "image/ship.png"
					myplan = new Sprite("plan", new controllSpriteSheetPainter(planCells, img), planBehavior);
					myplan.left = canvas.width / 2;
					myplan.top = canvas.height - (planSize().h / 2 + 10);
					sprites.push(myplan);
				},

				myplanReborn: function(myplan) {
					setTimeout(function() {
						myplan.visible = true;
						myplan.left = canvas.width / 2;
						myplan.top = canvas.height - (planSize().h / 2 + 10);
						myplan.fireLevel = 1;
						myplan.rotateAngle = 0;
						myplan.god = true;
						setTimeout(function() {
							myplan.god = false;
						}, 5000)
					}, 1000)
				},

				update: function() {
					var stage = this;
					var boomnum = 0,
						misslenum = 0;

					this.loading.loop();
					if(this.loading.getComplete()) {
						ctx.clearRect(0, 0, canvas.width, canvas.height);
					}
					missles.foreach(function() {
						var missle = this;
						sprites.foreach(function() {
							var bp = this;
							if(bp.name === "badPlan" && bp.visible && missle.visible) {
								var juli = Math.sqrt(Math.pow(missle.left - bp.left, 2) + Math.pow(missle.top - bp.top, 2));
								if(juli < (planSize().w / 2 + missle.width / 2) && missle.isgood) {
									missle.visible = false;
									bp.blood -= 50;
									if(bp.blood <= 0) {
										bp.visible = false;
										point += bp.badKind;
										boom(bp)
									}
								}
							}
						});

						if(missle.visible) {
							if(!missle.isgood && myplan.visible && !myplan.god) {
								var juli = Math.sqrt(Math.pow(missle.left - myplan.left, 2) + Math.pow(missle.top - myplan.top, 2));
								if(juli < (planSize().w / 2 + 3)) {
									myplan.visible = false;
									dieNum++;
									missle.visible = false;
									boom(myplan)
									stage.myplanReborn(myplan)
								}
							}
							misslenum++;
							this.paint();
						}
					});

					booms.foreach(function() {
						if(this.visible) {
							boomnum++;
							this.paint();
						}
					})

					sprites.foreach(function() {
						if(this.name === "food" && this.visible) {
							var tjuli = Math.sqrt(Math.pow(this.left - myplan.left, 2) + Math.pow(this.top - myplan.top, 2));
							if(tjuli < (myplan.width / 2 + this.width / 2)) {
								this.visible = false;
								switch(this.kind) {
									case "LevelUP":
										myplan.fireLevel = myplan.fireLevel >= 100 ? myplan.fireLevel : myplan.fireLevel + 1;
										break;
									case "SpeedUP":
										myplan.firePerFrame = myplan.firePerFrame <= 10 ? 10 : myplan.firePerFrame - 10;
										break;
									case "God":
										myplan.god = true;
										setTimeout(function() {
											myplan.god = false
										}, 5000);
										break;
									default:
										break;
								}
							}
						}
						if(this.name === "badPlan" && myplan.visible && !myplan.god) {
							var juli = Math.sqrt(Math.pow(this.left - myplan.left, 2) + Math.pow(this.top - myplan.top, 2));
							if(juli < planSize().w) {
								myplan.visible = false;
								dieNum++;
								this.visible = false;
								boom(this)
								boom(myplan)
								stage.myplanReborn(myplan);
							}
						}

						this.paint();
					});

					if(myplan) {
						ctx.fillStyle = "#FFF"
						ctx.font = "14px 微软雅黑";
						ctx.textAlign = "left";
						ctx.textBaseline = "middle";
						ctx.fillText("Level:" + (myplan.fireLevel === 4 ? "Max" : myplan.fireLevel) + "        Speed:" + ((80 - myplan.firePerFrame) === 70 ? "Max" : (80 - myplan.firePerFrame)), 0, canvas.height - 18);
						ctx.fillText("Points:" + point + "     死亡次数:" + dieNum, 0, 18);

						if(foodDate === null) {
							foodDate = new Date();
						} else {
							var nowFoodDate = new Date();
							//每个一秒产生一个道具
							if(nowFoodDate - foodDate > 1000) {
								var createFood = Math.random() < 0.5 ? true : false; //百分之五十的概率产生道具
								if(createFood && !eatfood.visible) {
									eatfood.left = Math.random() * canvas.width - 60 + 30;
									eatfood.top = -30;
									//子弹升级的概率为0.9
									//子弹加速的概率为0.05
									//保护罩的概率为0.05
									eatfood.kind = Math.random() > 0.1 ? "LevelUP" : (Math.random() > 0.5 ? "SpeedUP" : "God");
									eatfood.visible = true;
								}
								foodDate = nowFoodDate;
							}
						}
					}

					boomDom.innerHTML = "爆炸使用率(已使用/存储总量):" + boomnum + "/" + booms.length;
					missleDom.innerHTML = "子弹使用率(已使用/存储总量):" + misslenum + "/" + missles.length;
					
				},
                ID:0,
				loop: function() {
					var _this = this;
					this.update();
					globalID = RAF(function() {
						_this.loop();
					});
				},

				start: function() {
						this.init();
						this.loop();
				},
				
				stop: function() {
					cancelAnimationFrame(globalID);	
				},
			}

			stage.start();
```


---
###3.2 功能
```graph 

    B["开始游戏"]
    B-->C[显示菜单]
    C-->D(开始);
    C-->E(设置);
    C-->F(帮助);
    C-->G(关于);
    C-->H(退出); 
    D-->I(LevelUp包出现)
    D-->J(敌机出现)
    D-->K(子弹产生)
    E-->L(难度)
    E-->M(音量)
    E-->N(背景)

```

---
###3.3 性能 
  对CPU有一定要求 
###3.4 输入项  
用于游戏控制的按键： 
方向控制：键盘上 下 左 右键 开火：自动 旋转：Z C 

###3.5 输出项  
  游戏画面输出 
###3.6 算法  
碰撞测试：矩形相交 
飞行轨迹：正弦函数、直线函数 
###3.7 流程逻辑  
  游戏开始 ——> 游戏菜单 ——> 玩家移动 ——> 敌机产生 ——> 玩家开火 ——> 敌机开火 ——> 碰撞测试 ——> 分数累计 ——> 升级包 ——> 游戏菜单 

###3.8 存储分配  
  先将程序内存储的资源文件动态载入到内存中，而后显示在游戏界面。 

 
###3.9 测试计划  
 项目完成前模块测试主要由管理组长完成。项目功能完成后由小组两名成员进行总体项目测试，做到测试人员与编码人员相分离。    
###3.10 具体人员安排 
人员分配：小组的整体框架是由技术组长和管理组长给构建好的，然后每个小组成员在构建好的框架进行代码的编写。

- 李滔(*2014131219*)：框架的搭建、主要函数的实现、代码的整合
- 廖清林(*2014131218*)：帮助和关于
- 王淋藜(*2014131204*)：设置
- 王德平(*2014131217*)：各界面设计与美化 
- 刘云峰(*2014131215*)：需求分析、报告说明书撰写 

###3.11 尚未解决的问题 
 关卡、地图重置。




