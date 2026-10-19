<script>
  import { onMount } from 'svelte';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';

  let lang = $state('en');
  let menuOpen = $state(false);
  let activeProject = $state(null);
  let activeAcademic = $state(null);
  let activePoster = $state(null);

const t = {
    en: {
      nav: ['Projects', 'About', 'Experience', 'Resume', 'Contact'],
      navIds: ['projects','about','experience','resume','contact'],
      heroGreeting: "Hello, I'm",
      heroName: 'Shangyi Zhou',
      heroSub: 'UX Designer/Product Manager · Bridging Design, Technology & Cross-Functional Teams',
      heroDesc: "M.A. Digital Studies (HCI & Product Design) @ UChicago · Previously at L'Oréal R&I Shanghai",
      heroCta: 'View My Work',
      aboutTitle: 'About Me',
      aboutText: "I'm a product designer who builds what I design. At L'Oréal R&I Shanghai, I took an internal methodology platform from zero to launch — working with the Hair, Skin, and Make-Up teams, restructuring 100+ methodologies into a four-level taxonomy, and shipping the front end in React. I bring the same loop to my own projects, like CoDraft, an AI writing tool where the writer, not the model, makes every decision.",
      aboutText2: "I'm pursuing an M.A. in Digital Studies (HCI & Product Design) at the University of Chicago on a Dean's Scholarship, after studying Interdisciplinary Computing and the Arts at UC San Diego. My work sits where visual craft meets structure: information architecture that makes dense content easy to navigate, component libraries that keep a product consistent as it grows, and interaction details — motion, feedback, hover states — that I prototype and build myself.",
      skillsTitle: 'Skills',
      projectsTitle: 'Projects',
      expTitle: 'Experience',
      resumeTitle: 'Resume',
      resumeDesc: 'Download my full resume to learn more about my experience and skills.',
      resumeBtn: 'Download Resume',
      contactTitle: 'Get In Touch',
      contactDesc: "I'm currently looking for UI/UX, Product Design, Creative Visual Design, and Project Management opportunities. Let's connect!",
      linkedinLink: 'Connect on LinkedIn',
      instagramLink: 'Follow on Instagram',
      close: '✕ CLOSE',
      campusTitle: 'Campus',
      resumeBtnZh: 'Download CV (中文)',
      resumeBtnEn: 'Download Resume (EN)',
      academicTitle: 'Academic & Course Projects',
      viewProject: 'View Project',
    },
    zh: {
      nav: ['项目', '关于我', '经历', '简历', '联系'],
      navIds: ['projects','about','experience','resume','contact'],
      heroGreeting: '你好，我是',
      heroName: '周尚嶷',
      heroSub: '从UX设计走向产品管理 · 连接设计、技术与跨职能团队',
      heroDesc: "芝加哥大学 数字研究（Digital Studies）硕士｜人机交互与产品设计方向 · 曾实习于欧莱雅中国研发和创新中心",
      heroCta: '查看作品',
      aboutTitle: '关于我',
      aboutText: "我是一名会把自己的设计亲手做出来的产品设计师。在欧莱雅中国研发和创新中心，我把一个内部方法论平台从0做到上线——与护发、护肤、彩妆团队协作，将100+项方法论重构为四级分类体系，并用React完成前端交付。在自己的项目中我也沿用同样的闭环，比如CoDraft——一款AI写作工具，每一个决定都由写作者而不是模型来做。",
      aboutText2: "目前我在芝加哥大学攻读数字研究（Digital Studies）硕士，人机交互与产品设计方向，获院长奖学金；本科毕业于加州大学圣地亚哥分校跨学科计算与艺术专业。我的工作位于视觉表达与结构设计的交汇处：让密集内容易于浏览的信息架构、让产品在扩展中保持一致的组件库，以及我亲手做原型并实现的交互细节——动效、反馈与悬停状态。",
      skillsTitle: '技能',
      projectsTitle: '项目展示',
      expTitle: '实习经历',
      resumeTitle: '简历',
      resumeDesc: '下载我的完整简历，了解更多关于我的经历和技能。',
      resumeBtn: '下载简历',
      contactTitle: '联系我',
      contactDesc: '我正在寻找 UI/UX、产品设计、视觉创意设计、和项目管理方向的工作机会，欢迎联系！',
      linkedinLink: '领英主页',
      instagramLink: 'Instagram',
      close: '✕ 关闭',
      campusTitle: '校园经历',
      resumeBtnZh: '下载简历（中文版）',
      resumeBtnEn: 'Download Resume (EN)',
      academicTitle: '课程与学校项目',
      viewProject: '查看项目',
    }
  };

  const projects = [
    {
      id: 'loreal',
      titleEn: "L'Oréal Digital Methodology Encyclopedia",
      titleZh: '欧莱雅产品试验方法百科全书',
      tagEn: 'Product Design · Front-End Development · Project Management',
      tagZh: '产品设计 · 前端开发 · 项目管理',
      descEn: "A 0-to-1 internal platform housing 100+ product claims and testing methodologies for L'Oréal's R&I team, unifying information architecture, UI design, and front-end delivery into a single navigation system with a reusable component library. Independently led the full product lifecycle — from stakeholder alignment and UX requirements to prototype iteration and technical implementation with React and Figma, augmented by AI tooling.",
      descZh: '为欧莱雅研发创新部门从0到1搭建的内部平台，收录100+项产品声明与测试方法论，将信息架构、UI设计与前端交付整合进统一的导航系统与可复用组件库。独立主导产品全生命周期——从跨部门需求对齐、UX需求梳理，到原型迭代与基于React、Figma及AI工具的技术落地实现。',
      cover: '/images/Loreal/Loreal 5.jpg',
      coverVideo: '/images/Loreal/CoverLoreal.mp4',
      videos: ['/images/Loreal/video1.mp4', '/images/Loreal/video2.mp4', '/images/Loreal/video3.mp4', '/images/Loreal/video4.mp4'],
      imagesEn: ['/images/Loreal/Loreal 1.jpg','/images/Loreal/Loreal 2.jpg','/images/Loreal/Loreal 3.jpg','/images/Loreal/Loreal 4.jpg','/images/Loreal/Loreal 5.jpg','/images/Loreal/Loreal 6.jpg'],
      imagesZh: ['/images/Loreal/Loreal1CH.jpg','/images/Loreal/Loreal2CH.jpg','/images/Loreal/Loreal3CH.jpg','/images/Loreal/Loreal4CH.jpg','/images/Loreal/Loreal5CH.jpg','/images/Loreal/Loreal6CH.jpg'],
      color: '#9b7ed4',
      bg: '#0b0810',
      tools: ['React', 'Figma', 'AI Tooling', 'Information Architecture', 'Product Design', 'Project Management'],
    },
    {
      id: 'footnow',
      titleEn: 'FOOTNOW',
      titleZh: 'FOOTNOW',
      tagEn: 'APP Design · UX · Product Design',
      tagZh: 'APP设计 · 用户体验 · 产品设计',
      descEn: 'A smart soccer cleat app helping hobbyist players get game feedback, strengthen team bonds, and find nearby matches. Full UX research, personas, wireframes, and hi-fi prototypes.',
      descZh: '一款配合智能足球鞋的App，帮助业余球员获取比赛数据反馈、加强团队凝聚力，并轻松发现附近球友。包含完整用研、用户画像、线框图与高保真原型。',
      cover: '/images/footnow/Cover1.png',
      imagesEn: ['/images/footnow/1.jpg','/images/footnow/2.jpg','/images/footnow/3.jpg','/images/footnow/4.jpg','/images/footnow/5.jpg','/images/footnow/6.jpg'],
      imagesZh: ['/images/footnow/C1.jpg','/images/footnow/C2.jpg','/images/footnow/C3.jpg','/images/footnow/C4.jpg','/images/footnow/C5.jpg','/images/footnow/C6.jpg'],
      color: '#c8a45a',
      bg: '#0e0b04',
      tools: ['Figma', 'Adobe Photoshop', 'UX Research', 'Prototyping', 'Product Design'],
    },
    {
      id: 'codraft',
      titleEn: 'CoDraft:\nAI Writing Decomposer',
      titleZh: 'CoDraft · AI写作分解器',
      tagEn: 'AI Product Design · Full-Stack Development · UX',
      tagZh: 'AI产品设计 · 全栈开发 · 用户体验',
      descEn: 'An AI-powered writing companion that decomposes the drafting process into guided stages — outlining, structuring, and refining — powered by the Claude API. Independently taken from concept to production: product framing, UX flow, and full-stack build, with custom interaction details like magnetic cursor repulsion and 3D card tilt.',
      descZh: '一款基于 Claude API 的 AI 写作辅助工具，将写作过程拆解为大纲构建、结构梳理、语言润色等引导式阶段。独立完成从产品构思、交互设计到全栈开发的完整流程，并加入磁性光标排斥、卡片3D倾斜等自定义交互细节，提升写作过程中的沉浸感与掌控感。',
      cover: '/images/Decomposer/CoDraft 3.jpg',
      coverVideo: '/images/Decomposer/CoDraft Video.mp4',
      video: '/images/Decomposer/CoDraft Video.mp4',
      imagesEn: ['/images/Decomposer/CoDraft 1.jpg','/images/Decomposer/CoDraft 2.jpg','/images/Decomposer/CoDraft 3.jpg','/images/Decomposer/CoDraft 4.jpg'],
      imagesZh: ['/images/Decomposer/CoDraft 1 CH.jpg','/images/Decomposer/CoDraft 2 CH.jpg','/images/Decomposer/CoDraft 3 CH.jpg','/images/Decomposer/CoDraft 4 CH.jpg'],
      color: '#C40A12',
      bg: '#0e0403',
      link: 'https://writing-decomposer.vercel.app',
      tools: ['SvelteKit', 'Tailwind CSS', 'GSAP', 'Claude API', 'Product Design', 'Full-Stack Development'],
    },
{
      id: 'aigcatlas',
      titleEn: 'AIGC Atlas DashBoard',
      titleZh: 'AIGC艺术趋势Dashboard',
      tagEn: 'Data Visualization · Dashboard Design · Product Design',
      tagZh: '数据可视化 · 仪表盘设计 · 产品设计',
      descEn: 'An interactive dashboard visualizing AI-generated art style trends from 2022–2024, built on a curated dataset of AI artwork. Designed a full-screen, immersive interface housing seven distinct chart types — from trend lines to an interactive bubble world map — turning raw dataset into a legible visual narrative for researchers and enthusiasts.',
      descZh: '基于2022–2024年AI生成艺术数据集打造的交互式可视化看板。设计沉浸式全屏界面，整合趋势折线图、热力图、气泡世界地图等七种图表类型，将原始数据转化为易于理解的视觉叙事，服务于研究者与爱好者的探索需求。',
      cover: '/images/AIGC Atlas/AIGC Atlas 3.jpg',
      coverVideo: '/images/AIGC Atlas/AIGCAtlasVideo.mp4',
      video: '/images/AIGC Atlas/AIGCAtlasVideo.mp4',
      imagesEn: ['/images/AIGC Atlas/AIGC Atlas 1.jpg','/images/AIGC Atlas/AIGC Atlas 2.jpg','/images/AIGC Atlas/AIGC Atlas 3.jpg','/images/AIGC Atlas/AIGC Atlas 4.jpg'],
      imagesZh: ['/images/AIGC Atlas/AIGC Atlas 1 CH.jpg','/images/AIGC Atlas/AIGC Atlas 2 CH.jpg','/images/AIGC Atlas/AIGC Atlas 3 CH.jpg','/images/AIGC Atlas/AIGC Atlas 4 CH.jpg'],
      color: '#f0c94a',
      bg: '#0a0904',
      link: 'https://aigc-art-trends-dashboard.onrender.com/',
      tools: ['Python', 'Dash', 'Plotly', 'Data Visualization', 'Dashboard Design'],
    },
    {
      id: 'trackpack',
      titleEn: 'TrackPack',
      titleZh: 'TrackPack',
      tagEn: 'Product Design · APP Design · UX',
      tagZh: '产品设计 · APP设计 · 用户体验',
      descEn: 'An AI-powered smart suitcase and companion app using cameras and weight sensors to track belongings in real time, notifying users of missing items before departure.',
      descZh: '搭载AI摄像头与电子秤的智能行李箱及配套App，实时追踪物品进出与重量变化，在出发前提醒用户防止遗漏。',
      cover: '/images/trackpack/Cover2.png',
      imagesEn: ['/images/trackpack/7.jpg','/images/trackpack/8.jpg','/images/trackpack/9.jpg','/images/trackpack/10.jpg','/images/trackpack/11.jpg','/images/trackpack/12.jpg'],
      imagesZh: ['/images/trackpack/C7.jpg','/images/trackpack/C8.jpg','/images/trackpack/C9.jpg','/images/trackpack/C10.jpg','/images/trackpack/C11.jpg','/images/trackpack/C12.jpg'],
      color: '#e87d9b',
      bg: '#0e0408',
      tools: ['Figma', 'Adobe Photoshop', 'Product Design', 'User Research', 'Prototyping'],
    },
    {
      id: 'happyhour',
      titleEn: 'HappyHour',
      titleZh: 'HappyHour',
      tagEn: 'VR Design · User Experience',
      tagZh: 'VR设计 · 用户体验',
      descEn: 'A VR app encouraging moderate drinking while delivering an authentic bar atmosphere and social interactions — with user journey maps, personas, wireframes, and hi-fi VR UI.',
      descZh: '一款鼓励适度饮酒的虚拟现实App，提供真实感十足的酒吧体验与社交互动，含用户行为路径图、用户画像与高保真VR界面。',
      cover: '/images/happyhour/Cover3.png',
      imagesEn: ['/images/happyhour/13.jpg','/images/happyhour/14.jpg','/images/happyhour/15.jpg','/images/happyhour/16.jpg','/images/happyhour/17.jpg'],
      imagesZh: ['/images/happyhour/C13.jpg','/images/happyhour/C14.jpg','/images/happyhour/C15.jpg','/images/happyhour/C16.jpg','/images/happyhour/C17.jpg'],
      color: '#e26f50',
      bg: '#0e0604',
      tools: ['VR Design', 'Adobe Photoshop', 'Figma', 'UX Research', 'User Journey Map'],
    },
    {
      id: 'lanterns',
      titleEn: 'Lanterns But Light & Reunion',
      titleZh: 'Lanterns But Light & Reunion',
      tagEn: 'Interactive Art · Arduino · P5.JS',
      tagZh: '互动艺术 · Arduino · P5.JS',
      descEn: 'Two interactive artworks exploring cultural discontinuity — a physical Arduino light installation and a P5.js generative particle visualization.',
      descZh: '两件探讨文化断裂性与延续性的互动艺术作品——Arduino实体灯光装置与P5.js粒子可视化生成艺术。',
      cover: '/images/lanterns/Cover4.png',
      imagesEn: ['/images/lanterns/18.jpg','/images/lanterns/19.jpg','/images/lanterns/20.jpg','/images/lanterns/21.jpg','/images/lanterns/22.jpg','/images/lanterns/23.jpg'],
      imagesZh: ['/images/lanterns/C18-1.jpg','/images/lanterns/C19-1.jpg','/images/lanterns/C20-1.jpg','/images/lanterns/C21-1.jpg','/images/lanterns/C22-1.jpg','/images/lanterns/C23-1.jpg'],
      color: '#8fc44a',
      bg: '#050a02',
      tools: ['Arduino', 'P5.js', 'Interactive Art', 'Cultural Research'],
    },
  ];

  const academicProjects = [
    {
      id: 'ugarit',
      titleEn: 'Ugarit Tablet Inventory',
      titleZh: 'Ugarit 泥板文物数据库',
      tagEn: 'HTML · CSS · JavaScript · Web Development · Svelte',
      tagZh: 'HTML · CSS · JavaScript · 网页开发 · Svelte',
      descEn: 'A JavaScript/HTML/CSS web development project built with Svelte, querying the OCHRE archaeological database to display cuneiform tablet inventory from the kingdom of Ugarit — with an interactive MapLibre map, filterable ShadCN table, and dynamic UUID-based routes. Deployed on Vercel.',
      descZh: '使用 JavaScript、HTML、CSS 进行网页开发的 Svelte 应用，基于 OCHRE 考古数据库展示乌加里特王国楔形文字泥板文物清单，含 MapLibre 交互地图、可筛选数据表格与动态路由，部署于 Vercel。',
      cover: '/images/Academic/ugarit-1.png',
      images: ['/images/Academic/ugarit-1.png', '/images/Academic/ugarit-2.png', '/images/Academic/ugarit-3.png'],
      link: 'https://ugarit-app.vercel.app',
      tools: ['Front-End Development', 'Web Design', 'HTML', 'CSS', 'Javescript', 'Svelte', 'OCHRE SDK', 'MapLibre', 'ShadCN', 'Tailwind'],
      color: '#7ea8c4',
    },
    {
      id: 'met',
      titleEn: 'Met Museum Explorer',
      titleZh: '大都会博物馆艺术探索',
      tagEn: 'HTML · CSS · JavaScript · Web Development · Svelte 5',
      tagZh: 'HTML · CSS · JavaScript · 网页开发 · Svelte 5',
      descEn: 'A JavaScript/HTML/CSS web development project built with Svelte 5 + TypeScript that calls the Metropolitan Museum of Art API to let users explore fish and bird artworks. Features dynamic routing, random artwork selection, and nested detail pages. Deployed on Vercel.',
      descZh: '使用 JavaScript、HTML、CSS 进行网页开发的 Svelte 5 应用，调用大都会博物馆 API，让用户探索馆藏鱼类与鸟类主题艺术品，含动态路由、随机展示与嵌套详情页，部署于 Vercel。',
      cover: '/images/Academic/met-1.png',
      images: ['/images/Academic/met-1.png', '/images/Academic/met-2.png', '/images/Academic/met-3.png'],
      link: 'https://met-museum-app-uiux.vercel.app',
      tools: ['Front-End Development', 'Web Design', 'HTML', 'CSS', 'Javescript', 'Svelte', 'TypeScript', 'Tailwind', 'Met API'],
      color: '#c4a45a',
    },
    {
      id: 'brave',
      titleEn: 'Brave Buddies',
      titleZh: 'Brave Buddies',
      tagEn: 'Unity · C# · 2D Platformer · Multiplayer',
      tagZh: 'Unity · C# · 2D横版游戏 · 双人合作',
      descEn: 'A co-op 2D platformer built in Unity where two players — Wilo and Gabby — fight through forests and caves to rescue enslaved villagers. Features custom sprite animations, enemy AI, tilemap level design, and multiplayer controls.',
      descZh: '使用 Unity 开发的双人合作 2D 横版闯关游戏，玩家扮演 Wilo 与 Gabby 穿越森林与洞穴，击败恶魔救援村民，含自定义精灵动画、敌人 AI、Tilemap 关卡设计与双人控制系统。',
      cover: '/images/Academic/brave-1.png',
      images: ['/images/Academic/brave-1.png', '/images/Academic/brave-2.png', '/images/Academic/brave-3.png', '/images/Academic/brave-4.png'],
      link: 'https://kikoli0620.itch.io/brave-buddies',
      tools: ['Unity', 'C#', 'Figma', 'Adobe Photoshop', 'Tilemap', 'Sprite Animation'],
      color: '#a07ed4',
    },
    {
      id: 'cocktaildb',
      titleEn: 'Cocktail Database',
      titleZh: '鸡尾酒关系型数据库',
      tagEn: 'SQL · Relational Database · Data Management',
      tagZh: 'SQL · 关系型数据库 · 数据管理',
      descEn: 'A fully normalized relational database for cocktail management, built with SQL. Designed 15+ interconnected tables covering spirits, liqueurs, juices, syrups, glassware, and techniques. Wrote analytical queries including multi-table JOINs, GROUP BY aggregations, price analysis, and alcohol contribution calculations.',
      descZh: '使用 SQL 构建的鸡尾酒管理关系型数据库，设计 15+ 张相互关联的表，涵盖烈酒、利口酒、果汁、糖浆、玻璃器皿与调酒技法。编写多表 JOIN 查询、聚合分析、价格统计与酒精含量计算等分析性 SQL 语句。',
      cover: '/images/Academic/cocktail-1.png',
      images: ['/images/Academic/cocktail-1.png', '/images/Academic/cocktail-2.png', '/images/Academic/cocktail-3.png', '/images/Academic/cocktail-4.png'],
      link: 'https://github.com/alfalfa14/Data-Management-Cocktails-Project',
      tools: ['SQL', 'Database Design', 'Data Analysis', 'SQLite'],
      color: '#d4845a',
    },
    {
      id: 'spider',
      titleEn: 'Arduino Spider Robot',
      titleZh: 'Arduino 六足蜘蛛机器人',
      tagEn: 'Arduino · 3D Printing · Fusion 360 · PCB',
      tagZh: 'Arduino · 3D打印 · Fusion 360 · PCB焊接',
      descEn: 'A six-legged walking robot built from scratch — designed body parts in Fusion 360, printed with 3D printer, hand-soldered a custom PCB with ESP32, and programmed servo gait sequences in Arduino. A full hardware-to-firmware pipeline.',
      descZh: '从零构建的六足行走机器人——在 Fusion 360 中建模机身结构，3D 打印各关节部件，手工焊接含 ESP32 的自定义 PCB，并用 Arduino 编程舵机步态序列，完整覆盖硬件到固件的全流程。',
      cover: '/images/Academic/spider-3.jpg',
      images: ['/images/Academic/spider-5.jpg', '/images/Academic/spider-1.jpg', '/images/Academic/spider-2.jpg', '/images/Academic/spider-4.jpg', '/images/Academic/spider-3.jpg'],
      link: null,
      tools: ['Arduino', 'Fusion 360', '3D Printing', 'ESP32', 'PCB Design'],
      color: '#6ec49a',
    },
  ];

const experiences = [
    {
      companyEn: "L'Oréal",
      companyZh: '欧莱雅中国研发和创新中心',
      roleEn: 'Digital Project Designer/Manager Intern',
      roleZh: '数字化产品设计与开发实习生',
      period: '2026.06 – 2026.09',
      locationEn: 'Shanghai',
      locationZh: '上海',
      bulletsEn: [
        "Designed and shipped the **L'Oréal Digital Methodology Encyclopedia**, a 0-to-1 internal platform that helps R&I scientists across Hair, Skin, and Make-Up find product claims and testing methodologies in one place, consolidating **100+ methodologies** that were previously fragmented across teams.",
        "Conducted user research with each team to map how they organized their methods, then restructured the content into a **four-level taxonomy**, giving every methodology a predictable path from the homepage to its detail page.",
        "Produced **three competing Figma prototypes** and led a stakeholder vote to align teams on one direction, then delivered it through **3 iterative releases**, building the React front end with an AI-assisted workflow and a reusable template that keeps all methodology pages consistent.",
      ],
      bulletsZh: [
        "设计并上线**欧莱雅产品试验方法百科全书**——一款从0到1搭建的内部平台，帮助护发、护肤、彩妆三大品类的研发科学家在同一处查找产品声明与测试方法，整合了此前分散在各团队的**100+项方法论**。",
        "与各团队开展用户研究，梳理其方法论的组织方式，并将内容重构为**四级分类体系**，让每一项方法论都有一条从首页到详情页的清晰路径。",
        "产出**3套方向不同的Figma原型**并主导干系人投票，推动各团队就设计方向达成一致；随后通过**3轮迭代发布**完成交付，借助AI辅助工作流完成React前端开发，并搭建可复用模板，保证所有方法论页面的一致性。",
      ],
    },
    {
      companyEn: 'Lifang International Digital Technologies Co., Ltd.',
      companyZh: '力方国际数字科技有限公司',
      roleEn: 'UI Designer Intern',
      roleZh: 'UI 设计实习生',
      period: '2025.07 – 2025.08',
      locationEn: 'Chengdu',
      locationZh: '成都',
      bulletsEn: [
        "Designed **30+ hi-fi prototypes** for cultural digital interactive products, taking each from requirements and wireframes through usability testing to engineering handoff.",
        "Built a **20+ component** Figma library and unified the information architecture across products, cutting design-to-development handoff time by **30%** while working with the PM and a **20+ person** engineering team in agile sprints.",
      ],
      bulletsZh: [
        "为文化类数字互动产品设计**30+套高保真原型**，覆盖从需求梳理、线框图、可用性测试到工程交付的完整流程。",
        "搭建包含**20+组件**的Figma组件库并统一各产品的信息架构，将设计到开发的交付时间缩短**30%**；在敏捷迭代中与产品经理及**20+人**的开发团队紧密协作。",
      ],
    },
    {
      companyEn: 'USC – Prof. Aisling Kelliher, School of Cinematic Arts',
      companyZh: '南加州大学 Aisling Kelliher 教授',
      roleEn: 'Research Assistant',
      roleZh: 'AI 交互系统设计项目研究员',
      period: '2024.06 – 2024.07',
      locationEn: 'Los Angeles',
      locationZh: '洛杉矶',
      bulletsEn: [
        "Researched how AI-generated \"Memories\" albums in Apple Photos can resurface painful moments for users, analyzing **100+ cases and user behaviors** around emotion recognition and memory management.",
        "Translated findings into **10+ product recommendations** and an interaction prototype that gives users control to edit and filter AI-curated memories, informing the system's responsiveness and interaction design.",
      ],
      bulletsZh: [
        "研究苹果照片App中AI生成的“回忆”相册可能唤起用户痛苦记忆的问题，围绕情感识别与记忆管理分析**100+条案例与用户行为**。",
        "将研究结论转化为**10+条产品建议**与一套交互原型，让用户能够编辑和筛选AI生成的回忆内容，为系统的响应机制与交互设计提供依据。",
      ],
    },
    {
      companyEn: 'Nanjing Museum – Exhibition Department',
      companyZh: '南京博物院',
      roleEn: 'Exhibition Design Intern',
      roleZh: '陈列设计实习生',
      period: '2023.08 – 2023.09',
      locationEn: 'Nanjing',
      locationZh: '南京',
      bulletsEn: [
        "Planned the information architecture and visual presentation for **3 major exhibitions**, shaping how visitors encounter artifacts and interpretive content, in consultation with **10+ domain experts**.",
        "Organized **1,000+ archival materials** and **20+ bilingual documents** into a clear content hierarchy, coordinating with curators, designers, and logistics teams to bring each exhibition to opening.",
      ],
      bulletsZh: [
        "为**3场大型展览**规划信息架构与视觉呈现，设计观众接触文物与阐释内容的方式，期间与**10+位领域专家**沟通协作。",
        "将**1000+份档案资料**与**20+份中英双语文稿**整理为清晰的内容层级，并协调策展人、设计师与物流团队，推动每场展览顺利开展。",
      ],
    },
  ];

  const campus = [
    {
      companyEn: 'UCSD Envision Arts & Engineering Maker Studio',
      companyZh: '加州大学圣地亚哥分校 Envision Arts & Engineering Maker Studio',
      roleEn: 'Lab/Studio Assistant',
      roleZh: '实验室助理',
      period: '2024.01 – 2025.06',
      locationEn: 'San Diego',
      locationZh: '圣地亚哥',
      bulletsEn: [
        "Mentored **300+ students** in user-centered problem framing and rapid prototyping across engineering and design, helping bring **30+ projects** from concept to completion.",
      ],
      bulletsZh: [
        "指导**300+名学生**在工程与设计的交叉实践中进行以用户为中心的问题定义与快速原型设计，帮助**30+个项目**从概念走向落地。",
      ],
    },
  ];

  const skills = ['UX/UI Design', 'Interaction Design', 'HCI', 'Front-End Development', 'AI-assisted Development', 'Data Management/Visualization', 'User Research', 'Usability Testing', 'Product & Project Management', 'Game Design', 'Python', 'SQL', 'C++', 'C#', 'Java', 'JavaScript', 'HTML', 'CSS', 'React', 'Svelte', 'Figma', 'Photoshop', 'Illustrator', 'InDesign', 'Blender', 'Rhino', 'Sketch', 'Unreal Engine', 'Unity', 'MS Office'];

  const skillColors = ['#c8a45a', '#e87d9b', '#e26f50', '#8fc44a', '#7ea8c4', '#a07ed4', '#d4845a', '#6ec49a', '#C40A12', '#f0c94a'];

  function randomSkillColor() {
    return skillColors[Math.floor(Math.random() * skillColors.length)];
  }

  onMount(() => {
    gsap.registerPlugin(ScrollTrigger);
    gsap.from('.hero-greeting', { opacity: 0, y: 60, duration: 1, delay: 0.2, ease: 'power3.out' });
    gsap.from('.hero-name', { opacity: 0, y: 80, duration: 1.2, delay: 0.5, ease: 'power3.out' });
    gsap.from('.hero-sub', { opacity: 0, y: 40, duration: 1, delay: 0.9, ease: 'power3.out' });
    gsap.from('.hero-desc', { opacity: 0, y: 30, duration: 1, delay: 1.1, ease: 'power3.out' });
    gsap.from('.hero-cta', { opacity: 0, y: 30, duration: 1, delay: 1.3, ease: 'power3.out' });
    gsap.from('.hero-image', { opacity: 0, x: 80, duration: 1.4, delay: 0.4, ease: 'power3.out' });

    gsap.utils.toArray('.fade-up').forEach(el => {
      gsap.from(el, {
        scrollTrigger: { trigger: el, start: 'top 85%' },
        opacity: 0, y: 50, duration: 0.9, ease: 'power3.out'
      });
    });

    gsap.utils.toArray('.skill-tag').forEach((el, i) => {
      gsap.from(el, {
        scrollTrigger: { trigger: el, start: 'top 90%' },
        opacity: 0, y: 20, duration: 0.5, delay: i * 0.04, ease: 'power2.out'
      });
    });

    gsap.utils.toArray('.exp-item').forEach((el, i) => {
      gsap.from(el, {
        scrollTrigger: { trigger: el, start: 'top 85%' },
        opacity: 0, x: -40, duration: 0.9, delay: i * 0.15, ease: 'power3.out'
      });
    });

    const cursor = document.querySelector('.cursor');
    const cursorDot = document.querySelector('.cursor-dot');
    if (cursor && cursorDot) {
      document.addEventListener('mousemove', (e) => {
        gsap.to(cursor, { x: e.clientX, y: e.clientY, duration: 0.4, ease: 'power2.out' });
        gsap.to(cursorDot, { x: e.clientX, y: e.clientY, duration: 0.1 });
      });
    }
  });

  function scrollTo(id) {
    document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' });
    menuOpen = false;
  }

  function openProject(p) {
    activeProject = p;
    document.body.style.overflow = 'hidden';
  }

  function closeProject() {
    activeProject = null;
    document.body.style.overflow = '';
  }

  function openAcademic(p) {
    activeAcademic = p;
    document.body.style.overflow = 'hidden';
  }

  function closeAcademic() {
    activeAcademic = null;
    document.body.style.overflow = '';
  }

  function toggleLang() {
    lang = lang === 'en' ? 'zh' : 'en';
  }

  function currentImages(project) {
    return lang === 'zh' ? project.imagesZh : project.imagesEn;
  }

  const email = 'shz059' + '@' + 'uchicago.edu';

  // Split "**bold**" markers into segments for highlighted key data
  function rich(text) {
    return text.split(/(\*\*[^*]+\*\*)/).filter(Boolean).map(t =>
      t.startsWith('**') ? { b: true, t: t.slice(2, -2) } : { b: false, t }
    );
  }

  // Cover videos: muted autoplay loop, only while on screen
  function autoplayInView(node) {
    node.muted = true;
    const io = new IntersectionObserver(([entry]) => {
      if (entry.isIntersecting) node.play().catch(() => {});
      else node.pause();
    }, { threshold: 0.25 });
    io.observe(node);
    return { destroy() { io.disconnect(); } };
  }
</script>

<div class="cursor"></div>
<div class="cursor-dot"></div>

<!-- NAV -->
<nav class="fixed top-0 left-0 right-0 z-50 flex items-center justify-between px-8 py-5 nav-bar">
  <button onclick={()=>scrollTo('hero')} class="sy-logo">SY</button>
  <div class="hidden md:flex items-center gap-8">
    {#each t[lang].nav as item, i}
      <button onclick={()=>scrollTo(t[lang].navIds[i])} class="nav-link">{item}</button>
    {/each}
    <button onclick={toggleLang} class="lang-btn">{lang === 'en' ? '中文' : 'EN'}</button>
  </div>
  <button onclick={()=>menuOpen=!menuOpen} class="md:hidden flex flex-col gap-1.5 p-2">
    <div class="w-6 h-px bg-white transition-all" style="transform:{menuOpen?'rotate(45deg) translateY(6px)':'none'}"></div>
    <div class="w-6 h-px bg-white" style="opacity:{menuOpen?0:1}"></div>
    <div class="w-6 h-px bg-white transition-all" style="transform:{menuOpen?'rotate(-45deg) translateY(-6px)':'none'}"></div>
  </button>
</nav>

{#if menuOpen}
  <div class="fixed inset-0 z-40 bg-black flex flex-col items-center justify-center gap-8">
    {#each t[lang].nav as item, i}
      <button onclick={()=>scrollTo(t[lang].navIds[i])} class="text-white text-4xl tracking-widest uppercase" style="font-family:'Bebas Neue',sans-serif">{item}</button>
    {/each}
    <button onclick={()=>{toggleLang();menuOpen=false;}} class="text-white/50 text-base mt-4" style="font-family:'Space Mono',monospace">{lang==='en'?'切换中文':'Switch to EN'}</button>
  </div>
{/if}

<!-- HERO -->
<section id="hero" class="relative min-h-screen flex items-center overflow-hidden" style="background:#0a0a0a">
  <div class="noise-overlay"></div>
  <div class="vert-line" style="right:33.333%"></div>
  <div class="vert-line" style="left:33.333%"></div>

  <div class="relative z-10 w-full max-w-7xl mx-auto px-8 md:px-16 pt-32 pb-20 grid md:grid-cols-2 gap-12 items-center">
    <div>
      <p class="hero-greeting mono-sm mb-4" style="color:rgba(255,255,255,0.35)">{t[lang].heroGreeting}</p>
      <h1 class="hero-name display-font text-7xl md:text-9xl leading-none mb-6" style="color:white">{t[lang].heroName}</h1>
      <p class="hero-sub text-lg md:text-xl font-light mb-4 leading-relaxed" style="color:rgba(255,255,255,0.65)">{t[lang].heroSub}</p>
      <p class="hero-desc mono-sm tracking-wide mb-10" style="color:rgba(255,255,255,0.3)">{t[lang].heroDesc}</p>
      <button onclick={()=>scrollTo('projects')} class="hero-cta cta-btn">
        {t[lang].heroCta} <span class="arrow">→</span>
      </button>
    </div>
    <div class="hero-image relative flex justify-center">
      <img src="/images/photos/photo1.jpeg" alt="Shangyi Zhou" class="hero-photo w-full max-w-xs object-cover" style="aspect-ratio:3/4" />
      <div class="badge">
        <p class="mono-sm" style="color:rgba(255,255,255,0.45)">UChicago · UCSD</p>
      </div>
    </div>
  </div>

  <div class="scroll-hint">
    <div class="scroll-line"></div>
    <p class="mono-sm" style="color:rgba(255,255,255,0.22)">SCROLL</p>
  </div>
</section>

<!-- PROJECTS — image cards -->
<section id="projects" style="background:#0a0a0a;padding:8rem 2rem 4rem">
  <div class="max-w-7xl mx-auto">
    <p class="fade-up mono-sm mb-4" style="color:rgba(255,255,255,0.28)">01 / {t[lang].projectsTitle}</p>
    <h2 class="fade-up display-font text-5xl md:text-6xl mb-16" style="color:white">{t[lang].projectsTitle}</h2>

    <div class="proj-list">
      {#each projects as project, i}
        <div
          class="proj-card fade-up"
          style="--accent:{project.color}"
          onclick={() => openProject(project)}
          role="button"
          tabindex="0"
          onkeydown={(e) => e.key==='Enter' && openProject(project)}
        >
          <div class="proj-media">
            {#if project.coverVideo}
              <video
                src={project.coverVideo}
                class="proj-img proj-video"
                muted
                loop
                playsinline
                preload="metadata"
                aria-label={lang==='en' ? project.titleEn : project.titleZh}
                use:autoplayInView
              ></video>
            {:else}
              <img src={project.cover} alt={lang==='en' ? project.titleEn : project.titleZh} class="proj-img" loading="lazy" />
            {/if}
          </div>

          <div class="proj-info">
            <div class="proj-meta">
              <span class="mono-sm" style="color:rgba(255,255,255,0.25)">0{i+1}</span>
              <span class="mono-sm proj-tag">{lang==='en' ? project.tagEn : project.tagZh}</span>
            </div>
            <h3 class="display-font proj-title">{lang==='en' ? project.titleEn : project.titleZh}</h3>
            <p class="proj-desc">{lang==='en' ? project.descEn : project.descZh}</p>
            <div class="proj-tools">
              {#each project.tools as tool}
                <span class="mono-sm proj-tool">{tool}</span>
              {/each}
            </div>
            <p class="mono-sm proj-cta">{t[lang].viewProject} <span class="proj-arrow">→</span></p>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>


<!-- POSTER SECTION -->
<section style="background:#0a0a0a;padding:0 2rem 4rem">
  <div class="max-w-7xl mx-auto">
    <div style="display:flex;align-items:center;gap:1rem;margin-bottom:2rem;padding-top:1rem">
      <div style="width:1.5rem;height:1px;background:rgba(255,255,255,0.15)"></div>
      <p class="mono-sm" style="color:rgba(255,255,255,0.22)">
        {lang==='en' ? '↳ Graphic Design · Visual Communication' : '↳ 平面设计 · 视觉传达'}
      </p>
    </div>
    <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:1px;background:rgba(255,255,255,0.06)" class="poster-grid">
      {#each [
        { src: '/images/posters/Poster1.png', tagsEn: ['Adobe Photoshop', 'Figma', 'AIGC'], tagsZh: ['Adobe Photoshop', 'Figma', 'AIGC'] },
        { src: '/images/posters/Poster2.png', tagsEn: ['Adobe Photoshop', 'Figma'], tagsZh: ['Adobe Photoshop', 'Figma'] },
        { src: '/images/posters/Poster3.png', tagsEn: ['Adobe Photoshop', 'Figma'], tagsZh: ['Adobe Photoshop', 'Figma'] },
        { src: '/images/posters/Poster4.png', tagsEn: ['Adobe Photoshop', 'Figma'], tagsZh: ['Adobe Photoshop', 'Figma'] },
      ] as poster}
        <div
          class="poster-card"
          onclick={() => { activePoster = poster.src; document.body.style.overflow='hidden'; }}
          role="button"
          tabindex="0"
          onkeydown={(e) => { if(e.key==='Enter') { activePoster = poster.src; document.body.style.overflow='hidden'; } }}
        >
          <div class="poster-cover">
            <img src={poster.src} alt="Poster" class="poster-img" />
          </div>
          <div style="padding:0.9rem 1.2rem 1.2rem;display:flex;gap:0.4rem;flex-wrap:wrap">
            {#each (lang==='en' ? poster.tagsEn : poster.tagsZh) as tag}
              <span class="mono-sm" style="color:rgba(255,255,255,0.3);font-size:0.62rem">{tag}</span>
            {/each}
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- POSTER LIGHTBOX -->
{#if activePoster}
  <div
    style="position:fixed;inset:0;z-index:200;background:rgba(0,0,0,0.92);display:flex;align-items:center;justify-content:center;cursor:zoom-out"
    onclick={() => { activePoster = null; document.body.style.overflow=''; }}
    role="button"
    tabindex="0"
    onkeydown={(e) => { if(e.key==='Escape') { activePoster = null; document.body.style.overflow=''; } }}
  >
    <img src={activePoster} alt="Poster" style="max-height:92vh;max-width:92vw;object-fit:contain;box-shadow:0 0 80px rgba(0,0,0,0.8)" />
    <button
      onclick={() => { activePoster = null; document.body.style.overflow=''; }}
      style="position:fixed;top:1.5rem;right:2rem;font-family:'Space Mono',monospace;font-size:0.72rem;color:rgba(255,255,255,0.5);background:transparent;border:none;cursor:pointer;letter-spacing:0.15em"
    >✕ CLOSE</button>
  </div>
{/if}

<!-- ACADEMIC PROJECTS -->
<section style="background:#0a0a0a;padding:0 2rem 8rem">
  <div class="max-w-7xl mx-auto">

    <!-- 次级标题 -->
    <div style="display:flex;align-items:center;gap:1rem;margin-bottom:2rem;padding-top:1rem">
      <div style="width:1.5rem;height:1px;background:rgba(255,255,255,0.15)"></div>
      <p class="mono-sm" style="color:rgba(255,255,255,0.22)">
        {lang==='en' ? '↳ Academic & Course Projects' : '↳ 课程与学校项目'}
      </p>
    </div>

    <!-- 五格卡片 grid -->
    <div style="display:grid;grid-template-columns:repeat(5,1fr);gap:1px;background:rgba(255,255,255,0.06)" class="academic-grid">
      {#each academicProjects as proj}
        <div
          class="academic-card"
          onclick={() => openAcademic(proj)}
          role="button"
          tabindex="0"
          onkeydown={(e) => e.key==='Enter' && openAcademic(proj)}
        >
          <!-- Cover -->
          <div class="academic-cover">
            <img src={proj.cover} alt={proj.titleEn} class="academic-img" />
            <!-- Color accent bar -->
            <div style="position:absolute;bottom:0;left:0;right:0;height:2px;background:{proj.color};opacity:0.6"></div>
          </div>

          <!-- Info -->
          <div style="padding:1.25rem 1.5rem 1.5rem;display:flex;flex-direction:column;gap:0.6rem;flex:1">
            <p class="mono-sm" style="color:{proj.color};letter-spacing:0.1em;font-size:0.65rem">
              {lang==='en' ? proj.tagEn : proj.tagZh}
            </p>
            <h3 style="font-family:'Bebas Neue',sans-serif;font-size:1.3rem;color:white;line-height:1.1">
              {lang==='en' ? proj.titleEn : proj.titleZh}
            </h3>
            <p style="font-size:0.78rem;line-height:1.65;color:rgba(255,255,255,0.35)">
              {lang==='en'
                ? (proj.descEn.length > 110 ? proj.descEn.slice(0,110)+'…' : proj.descEn)
                : (proj.descZh.length > 55 ? proj.descZh.slice(0,55)+'…' : proj.descZh)}
            </p>
            <div style="display:flex;justify-content:space-between;align-items:center;margin-top:auto;padding-top:0.75rem;border-top:1px solid rgba(255,255,255,0.05)">
              <div style="display:flex;gap:0.4rem;flex-wrap:wrap">
                {#each proj.tools.slice(0,3) as tool, ti}
                  <span class="mono-sm" style="color:rgba(255,255,255,0.22);font-size:0.62rem">{tool}{ti < Math.min(proj.tools.length,3)-1 ? ' ·' : ''}</span>
                {/each}
              </div>
              <span style="font-size:0.8rem;color:{proj.color};opacity:0.65">↗</span>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<!-- ABOUT -->
<section id="about" style="background:#111;padding:8rem 2rem">
  <div class="max-w-7xl mx-auto grid md:grid-cols-2 gap-20 items-center">
    <div class="relative" style="padding-bottom:2.5rem;padding-right:2.5rem">
      <img src="/images/photos/photo2.jpeg" alt="Machu Picchu" class="fade-up w-full object-cover" style="aspect-ratio:1/1" />
      <img src="/images/photos/photo3.jpeg" alt="Envision Lab" class="fade-up absolute object-cover" style="width:10rem;height:10rem;bottom:0;right:0;border:4px solid #111" />
    </div>
    <div>
      <p class="fade-up mono-sm mb-4" style="color:rgba(255,255,255,0.28)">02 / {t[lang].aboutTitle}</p>
      <h2 class="fade-up display-font text-5xl md:text-6xl mb-8" style="color:white">{t[lang].aboutTitle}</h2>
      <p class="fade-up text-lg leading-relaxed mb-6" style="color:rgba(255,255,255,0.58)">{t[lang].aboutText}</p>
      <p class="fade-up text-lg leading-relaxed mb-12" style="color:rgba(255,255,255,0.58)">{t[lang].aboutText2}</p>
      <p class="fade-up mono-sm mb-6" style="color:rgba(255,255,255,0.28)">{t[lang].skillsTitle}</p>
      <div class="flex flex-wrap gap-2">
        {#each skills as skill}
          <span
            class="skill-tag mono-sm px-3 py-1.5 border cursor-default"
            style="color:rgba(255,255,255,0.5);border-color:rgba(255,255,255,0.1);transition:color 0.5s ease, border-color 0.5s ease"
            onmouseenter={(e) => {
              const c = randomSkillColor();
              e.currentTarget.style.color = c;
              e.currentTarget.style.borderColor = c;
            }}
            onmouseleave={(e) => {
              e.currentTarget.style.color = 'rgba(255,255,255,0.5)';
              e.currentTarget.style.borderColor = 'rgba(255,255,255,0.1)';
            }}
          >{skill}</span>
        {/each}
      </div>
    </div>
  </div>
</section>

<!-- EXPERIENCE -->
<section id="experience" style="background:#111;padding:8rem 2rem">
  <div class="max-w-7xl mx-auto">
    <p class="fade-up mono-sm mb-4" style="color:rgba(255,255,255,0.28)">03 / {t[lang].expTitle}</p>
    <h2 class="fade-up display-font text-5xl md:text-6xl mb-20" style="color:white">{t[lang].expTitle}</h2>
    <div>
      {#each experiences as exp}
        <div class="exp-item" style="border-top:1px solid rgba(255,255,255,0.07);padding:3rem 0;display:grid;grid-template-columns:1fr 2fr;gap:3rem">
          <div>
            <p class="mono-sm mb-2" style="color:rgba(255,255,255,0.28)">{exp.period}</p>
            <p class="mono-sm" style="color:rgba(255,255,255,0.22)">{lang==='en'?exp.locationEn:exp.locationZh}</p>
          </div>
          <div>
            <h3 class="display-font text-2xl mb-1" style="color:white">{lang==='en'?exp.roleEn:exp.roleZh}</h3>
            <p class="mono-sm mb-6" style="color:rgba(255,255,255,0.32)">{lang==='en'?exp.companyEn:exp.companyZh}</p>
            <ul style="display:flex;flex-direction:column;gap:0.75rem">
              {#each (lang==='en'?exp.bulletsEn:exp.bulletsZh) as bullet}
                <li style="display:flex;gap:0.75rem;font-size:0.875rem;line-height:1.65;color:rgba(255,255,255,0.52)">
                  <span style="color:rgba(255,255,255,0.18);flex-shrink:0;margin-top:0.1rem">—</span><span>{#each rich(bullet) as seg}{#if seg.b}<strong class="hl">{seg.t}</strong>{:else}{seg.t}{/if}{/each}</span>
                </li>
              {/each}
            </ul>
          </div>
        </div>
      {/each}
      <div style="border-top:1px solid rgba(255,255,255,0.07)"></div>
    </div>
  </div>
</section>

<!-- CAMPUS -->
<section style="background:#0a0a0a;padding:0 2rem 8rem">
  <div class="max-w-7xl mx-auto">
    <p class="fade-up mono-sm mb-12" style="color:rgba(255,255,255,0.28)">{t[lang].campusTitle}</p>
    <div>
      {#each campus as exp}
        <div class="exp-item" style="border-top:1px solid rgba(255,255,255,0.07);padding:3rem 0;display:grid;grid-template-columns:1fr 2fr;gap:3rem">
          <div>
            <p class="mono-sm mb-2" style="color:rgba(255,255,255,0.28)">{exp.period}</p>
            <p class="mono-sm" style="color:rgba(255,255,255,0.22)">{lang==='en'?exp.locationEn:exp.locationZh}</p>
          </div>
          <div>
            <h3 class="display-font text-2xl mb-1" style="color:white">{lang==='en'?exp.roleEn:exp.roleZh}</h3>
            <p class="mono-sm mb-6" style="color:rgba(255,255,255,0.32)">{lang==='en'?exp.companyEn:exp.companyZh}</p>
            <ul style="display:flex;flex-direction:column;gap:0.75rem">
              {#each (lang==='en'?exp.bulletsEn:exp.bulletsZh) as bullet}
                <li style="display:flex;gap:0.75rem;font-size:0.875rem;line-height:1.65;color:rgba(255,255,255,0.52)">
                  <span style="color:rgba(255,255,255,0.18);flex-shrink:0;margin-top:0.1rem">—</span><span>{#each rich(bullet) as seg}{#if seg.b}<strong class="hl">{seg.t}</strong>{:else}{seg.t}{/if}{/each}</span>
                </li>
              {/each}
            </ul>
          </div>
        </div>
      {/each}
      <div style="border-top:1px solid rgba(255,255,255,0.07)"></div>
    </div>
  </div>
</section>

<!-- RESUME -->
<section id="resume" style="background:#111;padding:8rem 2rem">
  <div class="max-w-7xl mx-auto text-center">
    <p class="fade-up mono-sm mb-4" style="color:rgba(255,255,255,0.28)">04 / {t[lang].resumeTitle}</p>
    <h2 class="fade-up display-font text-5xl md:text-6xl mb-8" style="color:white">{t[lang].resumeTitle}</h2>
    <p class="fade-up text-lg mb-12 max-w-xl mx-auto" style="color:rgba(255,255,255,0.38)">{t[lang].resumeDesc}</p>
    <div class="fade-up flex flex-col sm:flex-row gap-4 justify-center">
      <a href="/resume-zh.pdf" download="周尚嶷简历-中文版2026.pdf"
        class="inline-flex items-center gap-3 bg-white text-black px-8 py-4 text-sm font-bold tracking-widest uppercase hover:bg-white/85 transition-all">
        {t[lang].resumeBtnZh} ↓
      </a>
      <a href="/resume-en.pdf" target="_blank"
        class="inline-flex items-center gap-3 border border-white/30 text-white px-8 py-4 text-sm font-bold tracking-widest uppercase hover:bg-white hover:text-black transition-all">
        {t[lang].resumeBtnEn} ↓
      </a>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact" style="background:#111;padding:8rem 2rem">
  <div class="max-w-7xl mx-auto">
    <p class="fade-up mono-sm mb-4" style="color:rgba(255,255,255,0.28)">05 / {t[lang].contactTitle}</p>
    <h2 class="fade-up display-font text-5xl md:text-6xl mb-8" style="color:white">{t[lang].contactTitle}</h2>
    <p class="fade-up text-lg mb-12 max-w-2xl" style="color:rgba(255,255,255,0.38)">{t[lang].contactDesc}</p>
    <div class="fade-up flex flex-col sm:flex-row gap-6">
      <a href="/cdn-cgi/l/email-protection#dca7b9b1bdb5b0a1" class="inline-flex items-center gap-3 border border-white/20 text-white px-8 py-4 mono-sm tracking-widest hover:bg-white hover:text-black transition-all">
        ✉ {email}
      </a>
      <a href="https://www.linkedin.com/in/shangyi-zhou-2a02a4263/" target="_blank" class="inline-flex items-center gap-3 border border-white/20 px-8 py-4 mono-sm tracking-widest hover:border-white hover:text-white transition-all" style="color:rgba(255,255,255,0.45)">
        {t[lang].linkedinLink} ↗
      </a>
      <a href="https://www.instagram.com/alfalfa.z/" target="_blank" class="inline-flex items-center gap-3 border border-white/20 px-8 py-4 mono-sm tracking-widest hover:border-white hover:text-white transition-all" style="color:rgba(255,255,255,0.45)">
        {t[lang].instagramLink} ↗
      </a>
    </div>
  </div>
</section>

<footer style="background:#0a0a0a;border-top:1px solid rgba(255,255,255,0.05);padding:2rem">
  <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
    <p class="mono-sm" style="color:rgba(255,255,255,0.18)">© 2025 Shangyi Zhou · 周尚嶷</p>
    <p class="mono-sm" style="color:rgba(255,255,255,0.18)">{email}</p>
  </div>
</footer>

<!-- PROJECT MODAL (main) -->
{#if activeProject}
  <div class="modal-overlay" style="background:{activeProject.bg}">
    <div class="modal-topbar">
      <div style="display:flex;align-items:center;gap:1.5rem">
        <p class="mono-sm" style="color:{activeProject.color};letter-spacing:0.2em;text-transform:uppercase">
          {lang==='en' ? activeProject.tagEn : activeProject.tagZh}
        </p>
      </div>
      <div style="display:flex;align-items:center;gap:1rem">
        <button onclick={toggleLang} class="lang-btn-modal" style="border-color:{activeProject.color}50;color:{activeProject.color}">
          {lang==='en' ? '中文' : 'EN'}
        </button>
        <button onclick={closeProject} class="lang-btn-modal" style="border-color:{activeProject.color}50;color:{activeProject.color}">
          {t[lang].close}
        </button>
      </div>
    </div>

    <div style="max-width:72rem;margin:0 auto;padding:2rem 2rem 6rem">
      <div style="display:flex;gap:3rem;align-items:flex-start;margin-bottom:3rem;flex-wrap:wrap">
        <div style="flex:1 1 22rem;min-width:0">
          <h2 class="display-font" style="font-size:clamp(3rem,7vw,5.5rem);color:white;line-height:1;margin-bottom:1.5rem;white-space:pre-line">
            {lang==='en' ? activeProject.titleEn : activeProject.titleZh}
          </h2>
          <p style="color:rgba(255,255,255,0.55);font-size:1.05rem;line-height:1.75;margin-bottom:2rem;max-width:42rem">
            {lang==='en' ? activeProject.descEn : activeProject.descZh}
          </p>
          <div style="display:flex;flex-wrap:wrap;gap:0.5rem">
            {#each activeProject.tools as tool}
              <span class="mono-sm px-4 py-1.5" style="border:1px solid {activeProject.color}50;color:{activeProject.color}">{tool}</span>
            {/each}
          </div>
        </div>
        {#if activeProject.link}
          <div style="flex-shrink:0;display:flex;align-items:center">
            <a
              href={activeProject.link}
              target="_blank"
              style="display:inline-flex;align-items:center;gap:0.75rem;border:1px solid {activeProject.color};color:{activeProject.color};padding:1rem 2rem;font-family:'Space Mono',monospace;font-size:0.75rem;letter-spacing:0.18em;text-transform:uppercase;text-decoration:none;transition:background 0.25s, color 0.25s;white-space:nowrap"
              onmouseenter={(e) => {
                e.currentTarget.style.background = activeProject.color;
                e.currentTarget.style.color = '#000';
              }}
              onmouseleave={(e) => {
                e.currentTarget.style.background = 'transparent';
                e.currentTarget.style.color = activeProject.color;
              }}
            >
              {lang==='en' ? 'VISIT LIVE SITE' : '访问网站'} ↗
            </a>
          </div>
        {/if}
      </div>
      <div style="display:flex;flex-direction:column;gap:0.5rem">
        {#if activeProject.video}
          <video src={activeProject.video} controls playsinline style="width:100%;display:block"></video>
        {/if}
        {#if activeProject.videos}
          {#each activeProject.videos as vid}
            <video src={vid} controls playsinline style="width:100%;display:block"></video>
          {/each}
        {/if}
        {#each currentImages(activeProject) as img}
          <img src={img} alt="" style="width:100%;display:block;object-fit:contain" />
        {/each}
      </div>
    </div>
  </div>
{/if}

<!-- ACADEMIC MODAL -->
{#if activeAcademic}
  <div class="modal-overlay" style="background:#0d0d0d">
    <div class="modal-topbar">
      <p class="mono-sm" style="color:{activeAcademic.color};letter-spacing:0.2em;text-transform:uppercase">
        {lang==='en' ? activeAcademic.tagEn : activeAcademic.tagZh}
      </p>
      <div style="display:flex;align-items:center;gap:1rem">
        <button onclick={toggleLang} class="lang-btn-modal" style="border-color:rgba(255,255,255,0.2);color:rgba(255,255,255,0.45)">
          {lang==='en' ? '中文' : 'EN'}
        </button>
        <button onclick={closeAcademic} class="lang-btn-modal" style="border-color:rgba(255,255,255,0.15);color:rgba(255,255,255,0.45)">
          {t[lang].close}
        </button>
      </div>
    </div>

    <div style="max-width:72rem;margin:0 auto;padding:2rem 2rem 6rem">
      <div style="display:flex;gap:3rem;align-items:flex-start;margin-bottom:3rem;flex-wrap:wrap">
        <div style="flex:1 1 22rem;min-width:0">
          <h2 class="display-font" style="font-size:clamp(2.5rem,6vw,4.5rem);color:white;line-height:1;margin-bottom:1rem">
            {lang==='en' ? activeAcademic.titleEn : activeAcademic.titleZh}
          </h2>
          <p style="color:rgba(255,255,255,0.5);font-size:1rem;line-height:1.8;margin-bottom:1.5rem">
            {lang==='en' ? activeAcademic.descEn : activeAcademic.descZh}
          </p>
          <div style="display:flex;flex-wrap:wrap;gap:0.5rem">
            {#each activeAcademic.tools as tool}
              <span class="mono-sm px-4 py-1.5" style="border:1px solid {activeAcademic.color}40;color:{activeAcademic.color}">{tool}</span>
            {/each}
          </div>
        </div>
        {#if activeAcademic.link}
          <div style="flex-shrink:0;display:flex;align-items:center">
            <a
              href={activeAcademic.link}
              target="_blank"
              style="
                display:inline-flex;
                align-items:center;
                gap:0.75rem;
                border:1px solid {activeAcademic.color};
                color:{activeAcademic.color};
                padding:1rem 2rem;
                font-family:'Space Mono',monospace;
                font-size:0.75rem;
                letter-spacing:0.18em;
                text-transform:uppercase;
                text-decoration:none;
                transition:background 0.25s, color 0.25s;
                white-space:nowrap;
              "
              onmouseenter={(e) => {
                e.currentTarget.style.background = activeAcademic.color;
                e.currentTarget.style.color = '#000';
              }}
              onmouseleave={(e) => {
                e.currentTarget.style.background = 'transparent';
                e.currentTarget.style.color = activeAcademic.color;
              }}
            >
              {lang==='en' ? (activeAcademic.id === 'cocktaildb' ? 'VIEW ON GITHUB' : 'VISIT LIVE SITE') : (activeAcademic.id === 'cocktaildb' ? '查看 GitHub' : '访问网站')} ↗
            </a>
          </div>
        {/if}
      </div>
      <div style="display:flex;flex-direction:column;gap:0.5rem">
        {#each activeAcademic.images as img}
          <img src={img} alt="" style="width:100%;display:block;object-fit:contain" />
        {/each}
      </div>
    </div>
  </div>
{/if}

<style>
  @import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Space+Mono:wght@400;700&display=swap');

  :global(html) { scroll-behavior: smooth; }
  :global(body) { background: #0a0a0a; overflow-x: hidden; }

  .display-font { font-family: 'Bebas Neue', sans-serif; }
  .mono-sm { font-family: 'Space Mono', monospace; font-size: 0.72rem; letter-spacing: 0.12em; }

  .nav-bar {
    background: linear-gradient(to bottom, rgba(10,10,10,0.92), transparent);
    backdrop-filter: blur(8px);
  }
  .sy-logo { font-family:'Bebas Neue',sans-serif; font-size:1.25rem; color:white; letter-spacing:0.15em; }
  .nav-link { font-family:'Space Mono',monospace; font-size:0.72rem; color:white; letter-spacing:0.18em; text-transform:uppercase; transition:opacity 0.2s; }
  .nav-link:hover { opacity: 0.45; }
  .lang-btn { font-family:'Space Mono',monospace; font-size:0.72rem; color:white; border:1px solid rgba(255,255,255,0.35); padding:0.25rem 0.85rem; border-radius:999px; transition:all 0.2s; }
  .lang-btn:hover { background:white; color:black; }

  .noise-overlay {
    position:absolute; inset:0; opacity:0.038;
    background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='4'/%3E%3C/filter%3E%3Crect width='200' height='200' filter='url(%23n)'/%3E%3C/svg%3E");
    background-size:200px;
  }
  .vert-line { position:absolute; top:0; width:1px; height:100%; background:rgba(255,255,255,0.04); }

  .hero-photo { transition: filter 0.8s ease; }
  .hero-photo:hover { filter: sepia(0.5) saturate(2.5) hue-rotate(280deg) brightness(1.1); }

  .badge { position:absolute; bottom:1rem; right:1rem; padding:0.4rem 1rem; border:1px solid rgba(255,255,255,0.1); background:rgba(0,0,0,0.55); backdrop-filter:blur(6px); }

  .cta-btn { display:inline-flex; align-items:center; gap:0.75rem; background:white; color:black; padding:1rem 2rem; font-size:0.78rem; font-weight:700; letter-spacing:0.2em; text-transform:uppercase; transition:background 0.2s; }
  .cta-btn:hover { background:rgba(255,255,255,0.88); }
  .arrow { display:inline-block; transition:transform 0.3s; }
  .cta-btn:hover .arrow { transform:translateX(6px); }

  .scroll-hint { position:absolute; bottom:2rem; left:50%; transform:translateX(-50%); display:flex; flex-direction:column; align-items:center; gap:0.5rem; }
  .scroll-line { width:1px; height:4rem; background:linear-gradient(to bottom, transparent, rgba(255,255,255,0.28)); animation:pulse 2s ease-in-out infinite; }
  @keyframes pulse { 0%,100%{opacity:0.4} 50%{opacity:1} }

  .hl { color:rgba(255,255,255,0.92); font-weight:600; }

  /* Project cards */
  .proj-list { display:flex; flex-direction:column; gap:1.5rem; }
  .proj-card {
    display:grid;
    grid-template-columns: 1.4fr 1fr;
    gap:3rem;
    align-items:center;
    padding:2rem;
    background:#111;
    border:1px solid rgba(255,255,255,0.07);
    border-radius:4px;
    cursor:pointer;
    outline:none;
    transition:border-color 0.4s ease, background 0.4s ease;
  }
  .proj-card:hover { border-color:color-mix(in srgb, var(--accent) 45%, transparent); background:#141414; }
  .proj-card:focus-visible { border-color:var(--accent); }

  .proj-media { overflow:hidden; border-radius:2px; background:#0a0a0a; }
  .proj-img { width:100%; height:auto; display:block; transition:transform 0.6s ease; }
  .proj-card:hover .proj-img { transform:scale(1.025); }
  .proj-video { aspect-ratio:16 / 9; object-fit:cover; }

  .proj-info { display:flex; flex-direction:column; gap:1rem; min-width:0; }
  .proj-meta { display:flex; gap:1rem; align-items:baseline; }
  .proj-tag { color:var(--accent); line-height:1.6; }
  .proj-title {
    font-size:clamp(1.9rem, 3vw, 2.8rem);
    line-height:1;
    color:white;
    white-space:pre-line;
    transition:color 0.35s ease;
  }
  .proj-card:hover .proj-title { color:var(--accent); }
  .proj-desc {
    font-size:0.92rem;
    line-height:1.7;
    color:rgba(255,255,255,0.55);
    display:-webkit-box;
    -webkit-line-clamp:4;
    -webkit-box-orient:vertical;
    overflow:hidden;
  }
  .proj-tools { display:flex; flex-wrap:wrap; gap:0.4rem; }
  .proj-tool { font-size:0.62rem; padding:0.25rem 0.6rem; border:1px solid rgba(255,255,255,0.12); color:rgba(255,255,255,0.45); }
  .proj-cta { color:rgba(255,255,255,0.4); letter-spacing:0.18em; text-transform:uppercase; margin-top:0.25rem; transition:color 0.3s; }
  .proj-card:hover .proj-cta { color:var(--accent); }
  .proj-arrow { display:inline-block; transition:transform 0.3s; }
  .proj-card:hover .proj-arrow { transform:translateX(6px); }

  @media (max-width: 860px) {
    .proj-card { grid-template-columns:1fr; gap:1.5rem; padding:1.25rem; }
  }

  .academic-grid {
    border: 1px solid rgba(255,255,255,0.06);
  }

  /* Poster cards */
  .poster-grid {
    border: 1px solid rgba(255,255,255,0.06);
  }

  .poster-card {
    background: #0a0a0a;
    cursor: zoom-in;
    display: flex;
    flex-direction: column;
    transition: background 0.3s ease;
    outline: none;
  }
  .poster-card:hover { background: #111; }

  .poster-cover {
    position: relative;
    overflow: hidden;
    aspect-ratio: 1080 / 1500;
    background: #111;
  }
  .poster-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    transition: transform 0.5s ease, filter 0.5s ease;
    filter: brightness(0.6) saturate(0.6);
  }
  .poster-card:hover .poster-img {
    transform: scale(1.03);
    filter: brightness(1) saturate(1);
  }

  @media (max-width: 700px) {
    .poster-grid {
      grid-template-columns: repeat(2, 1fr) !important;
    }
  }

  .academic-card {
    background: #0a0a0a;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    transition: background 0.3s ease;
    outline: none;
  }
  .academic-card:hover { background: #111; }
  .academic-card:focus-visible { outline: 1px solid rgba(255,255,255,0.2); }

  .academic-cover {
    position: relative;
    overflow: hidden;
    aspect-ratio: 16 / 10;
    background: #111;
  }
  .academic-img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
    transition: transform 0.5s ease, filter 0.5s ease;
    filter: brightness(0.35) saturate(0.4);
  }
  .academic-card:hover .academic-img {
    transform: scale(1.04);
    filter: brightness(1) saturate(1);
  }

  .modal-overlay {
    position:fixed; inset:0; z-index:100; overflow-y:auto;
    animation: modalIn 0.35s cubic-bezier(0.4,0,0.2,1);
  }
  @keyframes modalIn {
    from { opacity:0; transform:translateY(30px); }
    to { opacity:1; transform:translateY(0); }
  }

  .modal-topbar {
    position:sticky; top:0; z-index:10;
    display:flex; justify-content:space-between; align-items:center;
    padding:1.25rem 2rem;
    background:rgba(0,0,0,0.6);
    backdrop-filter:blur(12px);
    border-bottom:1px solid rgba(255,255,255,0.06);
    max-width:100%;
  }

  .lang-btn-modal {
    font-family:'Space Mono',monospace;
    font-size:0.7rem;
    letter-spacing:0.15em;
    padding:0.35rem 0.9rem;
    border:1px solid;
    background:transparent;
    cursor:pointer;
    transition:opacity 0.2s;
  }
  .lang-btn-modal:hover { opacity:0.6; }

  .cursor { position:fixed; width:36px; height:36px; border:1px solid rgba(255,255,255,0.4); border-radius:50%; pointer-events:none; z-index:9999; top:0; left:0; transform:translate(-50%,-50%); display:none; transition:width 0.3s,height 0.3s; }
  .cursor-dot { position:fixed; width:4px; height:4px; background:white; border-radius:50%; pointer-events:none; z-index:9999; top:0; left:0; transform:translate(-50%,-50%); display:none; }
  @media (pointer:fine) { .cursor { display:block; } .cursor-dot { display:block; } }

  @media (max-width: 1100px) {
    .academic-grid {
      grid-template-columns: repeat(3, 1fr) !important;
    }
  }
  @media (max-width: 700px) {
    .academic-grid {
      grid-template-columns: repeat(2, 1fr) !important;
    }
  }
  @media (max-width: 480px) {
    .academic-grid {
      grid-template-columns: 1fr !important;
    }
  }
</style>