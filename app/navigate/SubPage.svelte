<script>
  import {goBack} from "svelte-native"
  export let article
</script>

  <page class="page">
      <stackLayout class="stack">
     
        <label class = "h1" text= "{article.title}" />
        <label class = "h1" text= "{article.author}" />
        <label class = "h1" text= "{article.description}" />
        <image 
          source = "{article.urlToImage}"
          stretch = "fill"
        />
        <button on:tap = { () =>goBack()} text="close"/>              //
      </stackLayout>
  </page>

<style>
 .stack{
     padding: 24;
 }

 .page{
   background-color: rgb(180, 180, 179);
 }
</style>