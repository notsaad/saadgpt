<script>
    import { onMount } from 'svelte';
  
    let sidebarItems = [
      { icon: '', text: 'SaadGPT', link: '/'},
      { icon: '', text: 'Read My Resume!', link: '/resume' }
    ];
  
    let historyItems = [
      { date: 'June 2024', items: ['This Site!'], link: 'https://www.github.com/notsaad/saadgpt_site' },
      { date: 'April 2024', items: ['Hotel Manager Site in Svelte'], link: 'https://www.github.com/dannyharani/HotelManager' },
      { date: 'February 2024', items: ['Sustain App'], link: 'https://devpost.com/software/sustain-5z8wkg'},
      { date: 'February 2023', items: ['Bandit Chrome Extension'], link: 'https://devpost.com/software/bandit'},
      { date: 'April 2019', items: ['Anxius Mental Health Game'], link: 'https://github.com/notsaad/anxius'},
    ];
  
  </script>
  
  <div class="layout">
    <aside class="sidebar">
      <nav>
      {#each sidebarItems as item}
        <a href={item.link} class="sidebar-item">
          <span class="icon">{item.icon}</span>
          <span>{item.text}</span>
        </a>
      {/each}
      </nav>
      <div class="history">
        {#each historyItems as section}
          <div class="history-section">
            <h3>{section.date}</h3>
            {#each section.items as item}
              <a href={section.link} class="history-item">
                {item}
              </a>
            {/each}
          </div>
        {/each}
      </div>
      <div class="upgrade-plan">
        <a class="email-button" href="mailto:saadmazharr@gmail.com">
          <span class="icon">✉️</span>
          Email Me!
        </a>
      </div>
    </aside>
  
    <main>
      <slot></slot>
    </main>
  
  </div>
  
  <style>

  /* @font-face{
    font-family: 'SohneLight';
    src: url(../../static/fonts/Sohne-Light.otf)
  }

  @font-face {
    font-family: 'SohneBold';
    src: url(../../static/fonts/Sohne-Bold.otf)
  } */
    
    .layout {
      font-family: 'SohneLight';
      display: flex;
      padding: 0%;
      margin: 0%;
      height: 100vh;
      color: #fff;
      background-color: #212121;
    }
  
    .sidebar {
      width: 260px;
      background-color: #171717;
      display: flex;
      flex-direction: column;
      padding: 10px;
    }

    .sidebar-item {
      text-align: center;
      font-family: 'SohneBold';
    }
  
    .sidebar-item, .history-item {
      padding: 10px;
      margin: 5px 0;
      cursor: pointer;
      text-decoration: none;
      color: inherit;
      display: block;
    }

    .sidebar-item:hover, .history-item:hover {
      background-color: #2A2B32;
      border-radius: 5px;
    }
  
    .history {
      flex-grow: 1;
      overflow-y: auto;
    }
  
    .history-section h3 {
      font-size: 0.8em;
      color: #8E8EA0;
      margin-top: 20px;
    }
  
    .upgrade-plan {
      font-family: 'SohneBold';
      margin-top: auto;
      padding: 10px;
    }
  
    .upgrade-plan a {
      background-color: #2A2B32;
      padding-top: 10px;
      padding-bottom: 10px;
      border: 1px solid #565869;
      color: #fff;
      border-radius: 5px;
      cursor: pointer;
      text-decoration: none;
      text-align: center;
    }

    .email-button{
      display: block;
      width: 100%;
    }

    .email-button:hover {
      background-color: #19C37D; /* Change the background color on hover */
      border-color: #19C37D; /* Optionally change the border color on hover */
      color: #fff; /* Ensure the text color stays white */
    }

    main {
      flex-grow: 1;
      padding: 20px;
      overflow-y: auto;
    }
  


  </style>