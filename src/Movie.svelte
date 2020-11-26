<script>
    export let Title;
    export let Poster;
    export let Year;

    import 'bulma/css/bulma.css';
    </script>
    
    <style>
      .user {
        padding: 5px;
        border: 1px solid #ddd;
        box-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
        border-radius: 5px;
        text-align: center;
      }

      .user:hover{
        box-shadow: 5px 5px 5px 5px rgba(0, 0, 0, 0.1);
      }
    
      img {
        border-radius: 5px;
        max-width: 150px;
      }
    
      h3 {
        font-size: 16px;
        margin: 0;
      }
    </style>
    
    <main>
    <div class="user">
    <img src="{Poster}" alt="{Title} PNG" />
    <h2 class='subtitle'>{Title}</h2>
    <h4>({Year})</h4>
    </div>
    </main>