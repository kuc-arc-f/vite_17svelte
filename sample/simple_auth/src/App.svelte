<script lang="ts">
import Router from 'svelte-spa-router'
//
import Layout from './components/Layout.svelte'
//
const pages = import.meta.glob('./pages/*.svelte', { eager: true })

const routes = Object.keys(pages).map((path) => {
  const name = path.match(/\.\/pages\/(.*)\.svelte$/)[1]
  let pathTmp = `/${name.toLowerCase()}`; 
  if(name === 'Home') { pathTmp ='/'};
  if(name === 'TestApiShow') { pathTmp ='/testapishow/:id'};
  return {
    name,
    path: pathTmp,
    component: pages[path].default,
  }
})
export let routeArray = {};
routes.forEach((item, idx) => {
  console.log(item)
  let path = item.path;
  let compo = item.component;
  //@ts-ignore
  routeArray[item.path] = compo;
});
console.log(routeArray);
</script>

<!-- -->
<Layout>
    <nav class="app_navi_wrap">
    {#each routes as item}
    <div>
      <a href={`/#${item.path}`}>{item.name}</a>
    </div>
    {/each}	
    </nav>
    <hr />
    <Router routes={routeArray} />
    <hr />
</Layout>

<style>
</style>
<!--
-->
  