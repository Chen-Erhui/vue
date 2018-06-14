<template>
	<div class="hello">
		<h1>{{ msg }}</h1>
		<div class="warp">
			<div class="box">
				<img id="img1" class="pic1" src="./img/pic1.png" alt="pic">
				<img id="img2" class="pic2" src="./img/pic2.png" alt="pic">
				<img id="img3" class="pic3" src="./img/pic3.png" alt="pic">
				<img id="img4" class="pic4" src="./img/pic4.png" alt="pic">
				<img id="img5" class="pic5" src="./img/pic5.png" alt="pic">
				<img id="img6" class="pic6" src="./img/pic6.png" alt="pic">
				<img id="img7" class="pic7" src="./img/pic7.png" alt="pic">
				<img id="img8" class="pic8" src="./img/pic8.png" alt="pic">
				<img id="img9" class="pic9" src="./img/pic9.png" alt="pic">
			</div>
		</div>
		<div class="btn">
			<div @click='pre' class="pre tt">向前</div>
			<div @click='next' class="next tt">向后</div>
		</div>
		<!--引入旋转木马轮播组件，主页面的轮播不太好看-.- -->
		<two :list="list" :cur-width="400" :all-width="800" :all-height="300"
	:cur-height="280" :scale="0.8"
	></two>
	</div>
</template>

<script>
	import two from './two'
	export default {
		name: 'HelloWorld',
		components: {
	    two
	  },
		data() {
			return {
				list: [{
						content: 1,
						color: 'red'
					},
					{
						content: 2,
						color: 'green'
					},
					{
						content: 3,
						color: 'blue'
					},
					{
						content: 4,
						color: '#66CC66'
					},
					{
						content: 5,
						color: 'black'
					},
					{
						content: 6,
						color: 'blue'
					}
				],
				msg: 'Welcome to Your Vue.js App',
				pic: ['pic1', 'pic2', 'pic3', 'pic4', 'pic5', 'pic6', 'pic7', 'pic8', 'pic9'],
				img: ['img1', 'img2', 'img3', 'img4', 'img5', 'img6', 'img7', 'img8', 'img9']
			}
		},
		methods: {
			change: function() {
				var _this = this
				this.img.map(function(n, i) {
					var img = document.getElementById(n)
					img.setAttribute('class', _this.pic[i])
				})
			},
			pre: function() {
				let frist = this.pic.shift() //将数组的第一个取出来
				this.pic.push(frist)
				this.change()
			},
			next: function() {
				let last = this.pic.pop()
				this.pic.unshift(last)
				this.change()
			}
		}
	}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
	.warp {
		/*margin-top: 350px;*/
		display: flex;
		justify-content: center;
		align-items: center;
	}
	
	.box {
		width: 400px;
		height: 250px;
		display: flex;
		justify-content: center;
		position: relative;
	}
	
	img {
		width: 400px;
		height: 250px;
		position: absolute;
		/*-webkit-box-reflect: below 10px -webkit-linear-gradient(transparent, transparent 70%, rgba(0, 0, 0, .5));*/
	}
	
	.pic1 {
		transition: all 1s;
		top: 40px;
		left: -400px;
		z-index: 96;
		opacity: 0.2;
		width: 320px;
		height: 170px;
	}
	
	.pic2 {
		transition: all .5s;
		top: 30px;
		left: -300px;
		z-index: 97;
		opacity: 0.4;
		width: 340px;
		height: 190px;
	}
	
	.pic3 {
		transition: all .5s;
		top: 20px;
		left: -200px;
		z-index: 98;
		opacity: 0.6;
		width: 360px;
		height: 210px;
	}
	
	.pic4 {
		transition: all .5s;
		top: 10px;
		left: -100px;
		z-index: 99;
		opacity: 0.8;
		width: 380px;
		height: 230px;
	}
	
	.pic5 {
		transition: all .5s;
		/*top: 0px;*/
		left: 0px;
		z-index: 100;
		opacity: 1;
		width: 400px;
		height: 250px;
	}
	
	.pic6 {
		transition: all .5s;
		top: 10px;
		left: 100px;
		z-index: 99;
		opacity: 0.8;
		width: 380px;
		height: 230px;
	}
	
	.pic7 {
		transition: all .5s;
		top: 20px;
		left: 200px;
		z-index: 98;
		opacity: 0.6;
		width: 360px;
		height: 210px;
	}
	
	.pic8 {
		transition: all .5s;
		top: 30px;
		left: 300px;
		z-index: 97;
		opacity: 0.4;
		width: 340px;
		height: 190px;
	}
	
	.pic9 {
		transition: all .5s;
		top: 40px;
		left: 400px;
		z-index: 96;
		opacity: 0.2;
		width: 320px;
		height: 170px;
	}
	
	.btn {
		width: 300px;
		margin: 0 auto;
		margin-top: 20px;
		line-height: 30px;
		text-align: center;
	}
	
	.tt {
		width: 60px;
		height: 30px;
		background-color: #048666;
		border-radius: 3px;
		color: #fff;
		cursor: pointer;
	}
	
	.pre {
		float: left;
	}
	
	.next {
		float: right;
	}
</style>