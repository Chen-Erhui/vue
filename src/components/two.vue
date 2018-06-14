<template>
	<div class="hello">
		<div class="cascade-list">
			<button @click="toggleDir" class="toggle">切换方向:{{dir}}</button>
			<div @mouseover="clearTimer" @mouseout="setTimer" v-for="(item, index) in items" class="item" :style="{width:item.width+'px',
		 height:item.height+'px',
			 left:item.left+'px',
				 bottom:item.bottom+'px',
					 'z-index':item.zIndex,
						 opacity:item.opacity,
							 'background-color':rlist[index].color
	}">
				<span :style="{'line-height':item.height+'px'}">{{rlist[index].content}}</span>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
		name: 'two',
		props: ['list', 'allWidth', 'allHeight', 'curHeight', 'curWidth', 'scale'],
		data() {
			var items = [];
			var rlist = this.copyArr(this.list);
			var level = Math.floor(this.list.length / 2);
	
			var lefts = rlist.slice(0, level);
			var rights = rlist.slice(level);
			var that = this;
			var leftGap = (this.allWidth - this.curWidth) / 2;
			var gap = leftGap / level;
			lefts.forEach(function(e, i) {
				var obj = {};
				obj.content = e.content;
				obj.left = i * gap;
				obj.zIndex = i + 1;
				obj.opacity = 1 / (level + 1 - i);
				obj.width = that.curWidth * Math.pow(that.scale, level - i);
				obj.height = that.curHeight * Math.pow(that.scale, level - i);
				obj.bottom = (that.allHeight - obj.height) / 2;
				items.push(obj);
			});
			rights.forEach(function(e, i) {
				var obj = {};
				obj.content = e.content;
				obj.width = that.curWidth * Math.pow(that.scale, i);
				obj.height = that.curHeight * Math.pow(that.scale, i);
				obj.left = that.allWidth - (level - i) * gap - obj.width;
				obj.zIndex = level - i + 1;
				obj.opacity = 1 / (i + 1);
				obj.bottom = (that.allHeight - obj.height) / 2;
				items.push(obj);
			});
			console.log(items);
			return {
				items: items,
				rlist: rlist,
				timer: null,
				dir: 'right'
			}
		},
		created() {
			this.setTimer();
		},
		methods: {
			copyArr: function(arr) {
				return arr.map((e) => {
					if(typeof e === 'object') {
						return Object.assign({}, e)
					} else {
						return e
					}
				})
			},
			setTimer: function() {
				var that = this;
				this.clearTimer();
				function cb() {
					that.timer = setTimeout(function() {
						if(that.dir == "right") {
							var pop = that.items.shift();
							that.items.push(pop);
						} else {
							var pop = that.items.pop();
							that.items.unshift(pop);
						}
						cb();
					}, 2000);
				}
				cb();
			},
			clearTimer: function() {
				if(this.timer) {
					clearTimeout(this.timer);
				}
			},
			toggleDir: function() {
				if(this.dir == 'right') {
					this.dir = 'left';
					return;
				}
				this.dir = 'right';
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.cascade-list {
		width: 800px;
		height: 300px;
		position: relative;
		margin: 0 auto;
	}
	
	.toggle {
		position: absolute;
		padding: .5em .8em;
		top: 0;
		left: 0;
	}
	
	.item {
		box-sizing: border-box;
		border: 1px solid #fff;
		position: absolute;
		display: block;
		background-color: blue;
		color: #fff;
		text-align: center;
		transition: all .8s ease;
	}
	
	.item span {
		transition: inherit;
		font-size: 60px;
	}
	
	.cascade-list .item:nth-child(2n) {
		/*
	background-color:red;
	*/
	}
</style>