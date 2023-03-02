# Link
[link](https://qoyie.github.io/Pythagorean-theorem-practice/)

# code

```js
function factors(n){
  if(n < 2)
    return []
  const prime_factors = []
  while(!(n&1)){
    n>>=1;
    prime_factors.push(2)
  }
  for(let p=3;;p+=2){
    if(p*p > n) break
    while(n % p == 0){
      prime_factors.push(p)
      n = Math.floor(n/p)
    }
  }
  if(n > 1)
    prime_factors.push(n)
  return prime_factors
}
function root(n){
  if(n < 2)
    return '' + n
  const prime_factors = factors(n)
  let base = 1
  let root = 1
  let prev = prime_factors[0];
  for(let i = 1; i < prime_factors.length; i++){
    if(prime_factors[i] == prev){
      base *= prev
      if(++i < prime_factors.length)
        prev = prime_factors[i]
      else
        prev = 1
    }else{
      root *= prev
      prev = prime_factors[i]
    }
  }
  root *= prev
  return (base==1?'':base)+(root==1?'':'√'+root)
}
const d = open().document
d.body.insertAdjacentHTML('beforeend',
`
<style>
details{
  display:none
}
#ddwn:checked~div>details{
  display:inline
}
body>div>span{
  display:none
}
#input:checked~div>span{
  display:inline
}
#input:checked~div>span>:valid+span::after{
  content:"正解"
}

#input:checked~div>span>:invalid+span::after{
  content:"不正解"
}
</style>
判定方法<br>
<input type="radio" name="validation" value="0" id="ddwn">
<label for="ddwn">
ドロップダウン
</label>
<br>
<input type="radio" name="validation" value="0" id="input">
<label for="input">
入力
</label>
<br>
`)
const b = d.createElement('button')
b.textContent='再生成'
b.addEventListener('click',main)
d.body.append(b)
const result = d.createElement('div')
d.body.append(result)
function main(){
  let buf=''
  for(let i = 0;i < 10; i++){
    const a = Math.floor(Math.random()*20) + 1
    const b = Math.floor(Math.random()*20) + 1
    const c = a + b
    const [A,B,C] = [a,b,a+b].map(root)
    const r = Math.random() < 0.5
    buf +=
`
${r?'他の一辺':'斜辺'}：${r?A:C} cm<br>
他の一辺：${B} cm
<span>
  ${r?'斜辺':'他の一辺'}：<input type="text" class="answer" pattern="${(r?C:A).replace('√','[rR]')}">
  <span><br></span>
</span>
<details>
  <summary>
    ${r?'斜辺':'他の一辺'}
  </summary>
  ${r?C:A} cm
</details>
<hr>
`
  }
  result.innerHTML=buf
}
main()
```
