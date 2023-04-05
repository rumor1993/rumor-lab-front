<script>
    import Body from "./Body.svelte";
</script>

<Body></Body>

<style lang="postcss">
    /* PC (해상도 1024px)*/ 
    @media all and (min-width:1024px) {
            :global(html) {
            width: 768px;
            margin: 0 auto;
        }
  
    } 

    /* 테블릿 가로, 테블릿 세로 (해상도 768px ~ 1023px)*/ 
    @media all and (min-width:768px) and (max-width:1023px) {
            :global(html) {
            width: 560px;
            margin: 0 auto;
        }
  
    } 

    /* 모바일 가로, 모바일 세로 (해상도 480px ~ 767px)*/ 
    @media all and (max-width:767px) {
            :global(html) {
            width: 420px;
            margin: 0 auto;
            display: flex;
            justify-content: center;
        }
  
    }
</style>