# Bookmark this

javascript:(()=%3E%7Bfunction%20e(e)%7Bif(e%3C2)return%5B%5D;let%20t=%5B%5D;for(;!(1&e);)e%3E%3E=1,t.push(2);for(let%20n=3;!(n*n%3Ee);n+=2)for(;e%25n==0;)t.push(n),e=Math.floor(e/n);return%20e%3E1&&t.push(e),t%7Dfunction%20t(t)%7Bif(t%3C2)return%22%22+t;let%20n=e(t),r=1,o=1,l=n%5B0%5D;for(let%20m=1;m%3Cn.length;m++)n%5Bm%5D==l?(r*=l,l=++m%3Cn.length?n%5Bm%5D:1):(o*=l,l=n%5Bm%5D);return(1==r?%22%22:r)+(1==(o*=l)?%22%22:%22%E2%88%9A%22+o)%7Dlet%20n=open().document,r=n.createElement(%22button%22);r.textContent=%22%E5%86%8D%E7%94%9F%E6%88%90%22,r.addEventListener(%22click%22,l),n.body.append(r);let%20o=n.createElement(%22div%22);function%20l()%7Blet%20e=%22%22;for(let%20n=0;n%3C10;n++)%7Blet%20r=Math.floor(20*Math.random())+1,l=Math.floor(20*Math.random())+1,%5Bm,u,a%5D=%5Br,l,r+l%5D.map(t),d=.5%3EMath.random();e+=(d?%22%E4%BB%96%E3%81%AE%E4%B8%80%E8%BE%BA%22:%22%E6%96%9C%E8%BE%BA%22)+%22%EF%BC%9A%22+(d?m:a)+%22%20cm%3Cbr%3E%E4%BB%96%E3%81%AE%E4%B8%80%E8%BE%BA%EF%BC%9A%22+u+%22%20cm%3Cdetails%3E%3Csummary%3E%22+(d?%22%E6%96%9C%E8%BE%BA%22:%22%E4%BB%96%E3%81%AE%E4%B8%80%E8%BE%BA%22)+%22%3C/summary%3E%22+(d?a:m)+%22%20cm%3C/details%3E%3Chr%3E%22%7Do.innerHTML=e%7Dn.body.append(o),l()%7D)()

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
