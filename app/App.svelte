<script>
    import {onMount} from "svelte"
    import {navigate} from "svelte-native"
    const apiKey = "e14f4ede420e450baafed861c6893a83"
    const NewsApi = `https://newsapi.org/v2/everything?q=bitcoin&from=2020-02-23&apiKey=${apiKey}`
    import SubPage from "./navigate/SubPage.svelte"

    let articles = []

    onMount (() => {
        fetch(NewsApi)
        .then(response => response.json())
        .then(json => {
            articles = json.articles
        })
        .catch(error => console.log(error))
    })

    const showPage = async(article) =>{
        await navigate({
            page: SubPage,
            props:{
                article:article
            }
        })
    }

</script>

<page class="page">
    <actionBar title="World Sports News" class="actionBar" />
    <stackLayout>

      <scrollView>
        <stackLayout class="articles" on:tap={() => showPage(SubPage)} >
          {#each articles as article}
            <flexboxLayout class="article" flexDirection="row">
              <image src="{article.urlToImage}" class="img-rounded img" stretch="fill" />
                <stackLayout class="lastStack">
                  <label textWrap={true} class="p text-center" text ="{article.title}" />
                  <label text ="{article.author}" class=" p text-center author"/>
                </stackLayout>
            </flexboxLayout>
            <label class="line"/>
          {:else}    
              <label text = "no fetching" class="h1" />
          {/each}
        </stackLayout> 
      </scrollView>

    </stackLayout>
</page>


<style>
    .actionBar{
        padding-left: 80;
        padding-right: 80;
        background-image: linear-gradient(to top, #adafb1, #ffffff);
    }

    .page{
        background-image: linear-gradient(to top, #bdc3c7, #5f7994);
    }

    .article{
        background-color: rgb(206, 206, 206);
        padding: 10;
        margin: 10;
        color: black;
        max-height: 100;
        width: 90%;
        border-radius: 10%;
    }
    .articles{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
    }
    .line{
        width: 80%;
        height: 1;
        background-color: white;
        margin: 15;
    }
    .img{
        margin: 0;
        width: 250;
        height: 130;
    }
    .author{
        bottom: 0;
        right: 0;
        font-size: 10;
        padding-top: 50;
        color: rgb(128, 87, 124);
        font-size: 18;
    }
</style>
