# JSX

```jsx
import Vue from 'vue'

new Vue({
	data () {
		return {
			str: 'hello',
			num: 1
		}
	},
	methods: {
		vIf () {
			if (this.num == 1) return <div>1</div>;
			else if (this.num == 2) return <div>2</div>;
			else return <div>3</div>;
		},
		handleClick (num) {
			console.log(num);
		}
	},
	render () {
		const tag = 'h' + this.num;
		return (<div>
			<tag>{ this.str }</tag>
			<h2 domPropsInnerHTML='<a>链接</a>'></h2>
			<h2 domPropsTextContent='<a>链接</a>'></h2>
			{ true ? <p>111</p> : <p>222</p> }
			{ this.vIf() }
			{ [1, 2, 3].map((item, index) => <li key={ index } ref='li' refInFor={ true }>{ item }</li>)}
			<button onClick={ () => { this.handleClick(123)} }>点击</button>
			<div class={ ['demo', 'foo'] } style={ {color: 'red'} }>demo</div>
			<input ref='input' v-model={ this.str }/>{ this.str }
		</div>)
	},
	mounted () {
		console.log(this.$refs);
	}
}).$mount('#app')
```
