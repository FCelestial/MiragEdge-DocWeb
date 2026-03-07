---
# https://vitepress.dev/reference/default-theme-home-page
layout: home
title: MiragEdge 文档中心

hero:
  name: "锐界幻境"
  text: "Minecraft生存服务器"
  tagline: 👼🏻远离困恼之地（锐界）和天堂般的境地（幻境），在数字荒漠中打造一片绿洲，让每个玩家都能找到属于自己的幻境
  image:
    src: /avatars/MiragEdge.png
    alt: MiragEdge
  actions:
    - theme: brand
      text: 玩家指南
      link: /manual/review.md
    - theme: alt
      text: 玩法介绍
      link: /features

features:
  - icon: 🚢
    title: 创新玩法
    details: 独家轻RPG系统、星露谷、附魔等多维度玩法
  - icon: 💾
    title: 高性能优化
    details: 高性能设备，先进架构优化，多线路负载均衡
  - icon: ❤️
    title: 优秀的社区
    details: 公益化的纯净体验，几乎7×24 小时管理在线，跨次元社交生态
  - icon: 🔧
    title: 稳定保障
    details: 长期开服不换档，每日增量备份 + 异地容灾，强力反作弊，自动白名单
  - icon: 🔄
    title: 持续更新
    details: 长期更新和优化，不断添加趣味功能与修复问题
---

## 硬件配置
> 英特尔i5 14600kf物理机，搭配360水冷 大核超频5.6GHz  
> 64G 高频内存  
> 宁波电信百兆主线路 + 宿迁三线BGP优化百兆线路(电信、移动、联通)  
> 三星数据中心级固态存储  

## 软件、备份策略、存档计划
> 使用Velocity反向代理下游Purpur服务端，实现一些高级的网络优化特性，稳定与性能兼备。  
> 应用全容器化管理，JumpServer堡垒机跳转，安全的多人协作。  
> 本地SQL数据库每天备份4次，每周进行一次虚拟机完整本地克隆备份，每月进行一次服务端完整云端备份。保障数据安全。  
> 梦始之空世界存档永久保存，计划性扩大世界边界。  

## 获取支持

- 加入玩家交流群获取帮助: 523914625
- 访问[GitHub仓库](https://github.com/fwindemiko/MiragEdge-DocWeb)提交问题或贡献代码

## 一些话
- 我只是个技术佬，语言学科非常烂，若文档有什么难读的地方，或者语句语法错误，还请麻烦指正。  
- 除了设计制作锐界幻境服务器，我还接受各种开服技术咨询，有偿问题解决，中小插件定制。  
- 我对锐界幻境的最终目标是“实现一个开放创新的服务器平台”。  
  ———狐风轩汐^F.windEmiko

<style scoped>
#star-canvas {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.VPHome {
  position: relative;
  z-index: 1;
}
</style>

<canvas id="star-canvas"></canvas>

<script setup>
import { onMounted, onUnmounted, nextTick } from 'vue'

// 普通封面图片列表
const normalImages = [
  '/title_img/icon-1.png',
  '/title_img/icon-1.png',
  '/title_img/icon-1.png',
  '/title_img/icon-2.png',
  '/title_img/icon-3.png',
]

// 隐藏款图片（出现概率是其他图片的1/10）
const hiddenImage = '/title_img/icon-dis.png'

let animationFrameId = null
let particles = []

onMounted(async () => {
  await nextTick()
  
  // 加权随机选择：dis.png 概率为其他图片的 1/5
  // 创建一个加权数组：其他图片各出现5次，隐藏款出现1次
  const weightedImages = [
    ...normalImages.map(img => Array(5).fill(img)).flat(), // 每张普通图片出现5次
    hiddenImage // 隐藏款出现1次
  ]
  
  // 随机选择一张图片
  const randomImage = weightedImages[Math.floor(Math.random() * weightedImages.length)]
  
  // 尝试多种选择器来查找 hero 图片
  const selectors = [
    '.VPHomeHero .VPImage img',
    '.VPHomeHero img',
    'main .VPImage img',
    '[alt="xingjiu"]'
  ]
  
  let heroImage = null
  for (const selector of selectors) {
    heroImage = document.querySelector(selector)
    if (heroImage) break
  }
  
  // 设置图片的函数
  const setImage = (imgElement, imageSrc) => {
    imgElement.src = imageSrc
    imgElement.alt = 'xingjiu'
    // 如果是 emoji4.png，缩放到 1.5 倍
    if (imageSrc.includes('emoji4.png')) {
      imgElement.style.transform = 'scale(1.5)'
      imgElement.style.transformOrigin = 'center'
    } else {
      // 重置其他图片的缩放
      imgElement.style.transform = ''
      imgElement.style.transformOrigin = ''
    }
  }
  
  // 如果找到了图片元素，替换它
  if (heroImage) {
    setImage(heroImage, randomImage)
  } else {
    // 如果没找到，延迟再试一次（等待 VitePress 渲染完成）
    setTimeout(() => {
      for (const selector of selectors) {
        heroImage = document.querySelector(selector)
        if (heroImage) {
          setImage(heroImage, randomImage)
          break
        }
      }
    }, 100)
  }
  
  // 初始化星星特效
  initStarEffect()
})

onUnmounted(() => {
  if (animationFrameId) {
    cancelAnimationFrame(animationFrameId)
  }
})

function initStarEffect() {
  const canvas = document.getElementById('star-canvas')
  if (!canvas) return
  
  const ctx = canvas.getContext('2d')
  let width = canvas.width = window.innerWidth
  let height = canvas.height = window.innerHeight
  
  const config = {
    spawnRate: 12,
    startSpeed: 0.6,
    attraction: 0.015,
    mouseForce: 0.05,
    maxMouseForce: 1.5,
    maxStarSpeed: 3.0,
    friction: 0.98,
    minDriftSpeed: 0.3,
    starBaseSize: 4,
    circleRadius: 600
  }
  
  const mouse = {
    x: undefined,
    y: undefined,
    vx: 0,
    vy: 0,
    lastX: 0,
    lastY: 0,
    isMoving: false,
    timer: null
  }
  
  const resize = () => {
    width = canvas.width = window.innerWidth
    height = canvas.height = window.innerHeight
  }
  
  window.addEventListener('resize', resize)
  
  window.addEventListener('mousemove', (e) => {
    mouse.x = e.x
    mouse.y = e.y
    mouse.vx = e.x - mouse.lastX
    mouse.vy = e.y - mouse.lastY
    mouse.lastX = e.x
    mouse.lastY = e.y
    mouse.isMoving = true
    
    clearTimeout(mouse.timer)
    mouse.timer = setTimeout(() => {
      mouse.vx = 0
      mouse.vy = 0
      mouse.isMoving = false
      mouse.x = undefined
      mouse.y = undefined
    }, 100)
  })
  
  class Star {
    constructor(centerX, centerY) {
      const angle = Math.random() * Math.PI * 2
      const radius = Math.random() * config.circleRadius * 0.3 + config.circleRadius * 0.1
      this.x = centerX + Math.cos(angle) * radius
      this.y = centerY + Math.sin(angle) * radius
      
      const driftAngle = angle + (Math.random() - 0.5) * 0.5
      const speed = config.startSpeed + Math.random() * 0.3
      
      this.vx = Math.cos(driftAngle) * speed
      this.vy = Math.sin(driftAngle) * speed
      
      this.size = Math.random() * 5 + config.starBaseSize
      this.life = 1
      this.decay = Math.random() * 0.001 + 0.0015
      this.hue = Math.random() * 60 + 180
    }
    
    draw(ctx) {
      ctx.save()
      ctx.translate(this.x, this.y)
      ctx.rotate(this.life * 0.5)
      
      ctx.beginPath()
      const r = this.size
      ctx.moveTo(0, -r)
      ctx.quadraticCurveTo(0, 0, r, 0)
      ctx.quadraticCurveTo(0, 0, 0, r)
      ctx.quadraticCurveTo(0, 0, -r, 0)
      ctx.quadraticCurveTo(0, 0, 0, -r)
      ctx.closePath()
      
      const gradient = ctx.createRadialGradient(0, 0, 0, 0, 0, r)
      gradient.addColorStop(0, `hsla(${this.hue}, 80%, 80%, ${this.life})`)
      gradient.addColorStop(1, `hsla(${this.hue}, 80%, 50%, ${this.life})`)
      
      ctx.fillStyle = gradient
      ctx.fill()
      ctx.restore()
    }
    
    update() {
      if (mouse.x !== undefined) {
        const dx = mouse.x - this.x
        const dy = mouse.y - this.y
        const distance = Math.sqrt(dx*dx + dy*dy)
        
        if (distance < 300) {
          const forceX = dx / distance
          const forceY = dy / distance
          
          this.vx += forceX * config.attraction
          this.vy += forceY * config.attraction
          
          if (mouse.isMoving) {
            let pushX = mouse.vx * config.mouseForce
            let pushY = mouse.vy * config.mouseForce
            
            const pushStrength = Math.sqrt(pushX * pushX + pushY * pushY)
            if (pushStrength > config.maxMouseForce) {
              const scale = config.maxMouseForce / pushStrength
              pushX *= scale
              pushY *= scale
            }
            
            this.vx += pushX
            this.vy += pushY
          }
        }
      }
      
      this.vx *= config.friction
      this.vy *= config.friction
      
      const currentSpeed = Math.sqrt(this.vx * this.vx + this.vy * this.vy)
      if (currentSpeed > config.maxStarSpeed) {
        const scale = config.maxStarSpeed / currentSpeed
        this.vx *= scale
        this.vy *= scale
      }
      
      if (currentSpeed < config.minDriftSpeed) {
        const heroImage = document.querySelector('.VPHomeHero .VPImage img') || 
                         document.querySelector('.VPHomeHero img')
        if (heroImage) {
          const rect = heroImage.getBoundingClientRect()
          const centerX = rect.left + rect.width / 2
          const centerY = rect.top + rect.height / 2
          const angleToCenter = Math.atan2(this.y - centerY, this.x - centerX)
          this.vx += Math.cos(angleToCenter) * 0.005
          this.vy += Math.sin(angleToCenter) * 0.005
        }
      }
      
      this.x += this.vx
      this.y += this.vy
      this.hue += 0.2
      this.life -= this.decay
    }
  }
  
  let frame = 0
  
  const animate = () => {
    animationFrameId = requestAnimationFrame(animate)
    
    ctx.clearRect(0, 0, width, height)
    
    ctx.globalCompositeOperation = 'lighter'
    
    frame++
    
    // 获取图标位置
    const heroImage = document.querySelector('.VPHomeHero .VPImage img') || 
                     document.querySelector('.VPHomeHero img')
    
    if (heroImage && frame % config.spawnRate === 0) {
      const rect = heroImage.getBoundingClientRect()
      const centerX = rect.left + rect.width / 2
      const centerY = rect.top + rect.height / 2
      particles.push(new Star(centerX, centerY))
    }
    
    for (let i = particles.length - 1; i >= 0; i--) {
      const p = particles[i]
      p.update()
      p.draw(ctx)
      
      if (p.life <= 0) {
        particles.splice(i, 1)
      }
    }
    
    ctx.globalCompositeOperation = 'source-over'
  }
  
  animate()
}
</script>