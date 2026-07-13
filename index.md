---
layout: default
title: Hoooon22's Portfolio
nav_order: 1
description: "김지훈 - 백엔드 개발자 포트폴리오"
permalink: /
---

<style>
/* 기본 스타일 리셋 및 변수 */
:root {
  --primary: #2563eb;
  --primary-dark: #1d4ed8;
  --secondary: #64748b;
  --accent: #0ea5e9;
  --background: #f8fafc;
  --surface: #ffffff;
  --text: #1e293b;
  --text-muted: #64748b;
  --border: #e2e8f0;
  --gradient-1: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  --gradient-2: linear-gradient(135deg, #2563eb 0%, #0ea5e9 100%);
}

/* 히어로 섹션 */
.hero-section {
  background: var(--gradient-1);
  padding: 80px 40px;
  border-radius: 24px;
  margin-bottom: 60px;
  position: relative;
  overflow: hidden;
}

.hero-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}

.hero-content {
  position: relative;
  z-index: 1;
  max-width: 800px;
}

.hero-tagline {
  color: rgba(255,255,255,0.9);
  font-size: 1.1rem;
  letter-spacing: 2px;
  text-transform: uppercase;
  margin-bottom: 16px;
}

.hero-title {
  color: white;
  font-size: 3.5rem;
  font-weight: 800;
  margin: 0 0 24px 0;
  line-height: 1.1;
}

.hero-subtitle {
  color: rgba(255,255,255,0.95);
  font-size: 1.5rem;
  font-weight: 400;
  margin-bottom: 32px;
  line-height: 1.6;
}

.hero-keywords {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  margin-bottom: 32px;
}

.keyword-badge {
  background: rgba(255,255,255,0.2);
  backdrop-filter: blur(10px);
  color: white;
  padding: 8px 20px;
  border-radius: 50px;
  font-size: 0.95rem;
  font-weight: 500;
  border: 1px solid rgba(255,255,255,0.3);
}

.hero-cta {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}

.cta-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 14px 28px;
  border-radius: 12px;
  font-size: 1rem;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
}

.cta-primary {
  background: white;
  color: #667eea;
}

.cta-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.2);
}

.cta-secondary {
  background: transparent;
  color: white;
  border: 2px solid rgba(255,255,255,0.5);
}

.cta-secondary:hover {
  background: rgba(255,255,255,0.1);
  border-color: white;
}

/* 섹션 공통 */
.section {
  margin-bottom: 60px;
}

.section-header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 32px;
}

.section-icon {
  width: 48px;
  height: 48px;
  background: var(--gradient-2);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

.section-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: var(--text);
  margin: 0;
}

/* 핵심 역량 섹션 */
.competency-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
}

.competency-card {
  background: var(--surface);
  border-radius: 16px;
  padding: 28px;
  border: 1px solid var(--border);
  transition: all 0.3s ease;
}

.competency-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 12px 40px rgba(0,0,0,0.08);
  border-color: var(--primary);
}

.competency-icon {
  width: 56px;
  height: 56px;
  background: linear-gradient(135deg, #e0e7ff 0%, #c7d2fe 100%);
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  margin-bottom: 20px;
}

.competency-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 12px;
}

.competency-desc {
  color: var(--text-muted);
  font-size: 0.95rem;
  line-height: 1.6;
  margin: 0;
}

/* 대표 프로젝트 섹션 */
.featured-project {
  background: var(--surface);
  border-radius: 20px;
  overflow: hidden;
  border: 1px solid var(--border);
  margin-bottom: 32px;
  transition: all 0.3s ease;
}

.featured-project:hover {
  box-shadow: 0 20px 60px rgba(0,0,0,0.1);
}

.project-banner {
  height: 8px;
}

.project-content {
  display: flex;
  flex-direction: column;
  gap: 32px;
  padding: 40px;
}

@media (max-width: 768px) {
  .project-content {
    padding: 24px;
  }
}

.project-visual {
  position: relative;
  max-height: 300px;
  border-radius: 12px;
}

.project-visual img {
  width: 100%;
  max-height: 300px;
  object-fit: contain;
  border-radius: 12px;
}

.project-badge {
  position: absolute;
  top: -8px;
  left: 12px;
  background: var(--primary);
  color: white;
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  z-index: 10;
  box-shadow: 0 2px 8px rgba(0,0,0,0.15);
}

.project-info h3 {
  font-size: 1.6rem;
  font-weight: 700;
  color: var(--text);
  margin: 0 0 8px 0;
}

.project-period {
  color: var(--text-muted);
  font-size: 0.9rem;
  margin-bottom: 16px;
}

.project-summary {
  color: var(--text);
  font-size: 1.05rem;
  line-height: 1.7;
  margin-bottom: 20px;
}

.project-highlight {
  background: #f0f9ff;
  border-left: 4px solid var(--accent);
  padding: 16px 20px;
  border-radius: 0 12px 12px 0;
  margin-bottom: 20px;
}

.project-highlight h4 {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--accent);
  margin: 0 0 8px 0;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.project-highlight p {
  color: var(--text);
  font-size: 0.95rem;
  margin: 0;
  line-height: 1.5;
}

.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.tech-tag {
  background: #f1f5f9;
  color: var(--secondary);
  padding: 6px 14px;
  border-radius: 8px;
  font-size: 0.85rem;
  font-weight: 500;
}

.project-links {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

.project-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 10px 20px;
  border-radius: 10px;
  font-size: 0.9rem;
  font-weight: 500;
  text-decoration: none;
  transition: all 0.2s ease;
}

.link-primary {
  background: var(--primary);
  color: white;
}

.link-primary:hover {
  background: var(--primary-dark);
}

.link-secondary {
  background: #f1f5f9;
  color: var(--text);
}

.link-secondary:hover {
  background: #e2e8f0;
}

/* 기타 프로젝트 그리드 */
.other-projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.mini-project-card {
  background: var(--surface);
  border-radius: 14px;
  padding: 24px;
  border: 1px solid var(--border);
  transition: all 0.3s ease;
}

.mini-project-card:hover {
  border-color: var(--primary);
  transform: translateY(-2px);
}

.mini-project-image {
  width: 100%;
  height: 140px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 16px;
}

.mini-project-images {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
}

.mini-project-images img {
  flex: 1;
  height: 100px;
  object-fit: cover;
  border-radius: 8px;
}

.mini-project-links {
  display: flex;
  gap: 8px;
  margin-top: 12px;
  flex-wrap: wrap;
}

.mini-link {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 0.8rem;
  font-weight: 500;
  text-decoration: none;
  background: #f1f5f9;
  color: var(--text);
  transition: all 0.2s ease;
}

.mini-link:hover {
  background: #e2e8f0;
}

/* 운영 중인 서비스 섹션 */
.live-services {
  margin-bottom: 20px;
}

.live-services-title {
  font-size: 0.9rem;
  font-weight: 600;
  color: var(--text-muted);
  margin-bottom: 12px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.service-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.service-item {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 16px;
  background: #f8fafc;
  border-radius: 10px;
  border: 1px solid var(--border);
  transition: all 0.2s ease;
  text-decoration: none;
  color: inherit;
}

.service-item:hover {
  border-color: var(--primary);
  background: #f0f9ff;
  transform: translateX(4px);
}

.service-icon {
  width: 36px;
  height: 36px;
  background: var(--gradient-2);
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.service-info {
  flex: 1;
}

.service-name {
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text);
  margin-bottom: 2px;
}

.service-desc {
  font-size: 0.85rem;
  color: var(--text-muted);
  margin: 0;
}

.mini-project-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 12px;
}

.mini-project-title {
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--text);
  margin: 0;
}

.mini-project-year {
  color: var(--text-muted);
  font-size: 0.85rem;
}

.mini-project-desc {
  color: var(--text-muted);
  font-size: 0.9rem;
  line-height: 1.5;
  margin-bottom: 16px;
}

.mini-tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.mini-tech {
  background: #f8fafc;
  color: var(--secondary);
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 0.8rem;
}

/* 기술 스택 섹션 */
.skills-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
}

.skill-category {
  background: var(--surface);
  border-radius: 14px;
  padding: 24px;
  border: 1px solid var(--border);
}

.skill-category-title {
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.5px;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.skill-list {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-item {
  background: var(--gradient-2);
  color: white;
  padding: 8px 16px;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 500;
}

/* 연락처 섹션 */
.contact-section {
  background: var(--gradient-1);
  border-radius: 20px;
  padding: 60px 40px;
  text-align: center;
}

.contact-title {
  color: white;
  font-size: 2rem;
  font-weight: 700;
  margin-bottom: 16px;
}

.contact-subtitle {
  color: rgba(255,255,255,0.9);
  font-size: 1.1rem;
  margin-bottom: 32px;
}

.contact-links {
  display: flex;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
}

.contact-link {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  background: white;
  color: #667eea;
  padding: 14px 28px;
  border-radius: 12px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s ease;
}

.contact-link:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.2);
}

/* 반응형 */
@media (max-width: 768px) {
  .hero-section {
    padding: 50px 24px;
  }

  .hero-title {
    font-size: 2.2rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }
}
</style>

<!-- 히어로 섹션: 첫인상을 결정하는 표지 -->
<div class="hero-section">
  <div class="hero-content">
    <p class="hero-tagline">Backend Developer</p>
    <h1 class="hero-title">안녕하세요,<br>김지훈입니다.</h1>
    <p class="hero-subtitle">
      <strong>"문제를 발견하고, 해결하고, 서비스로 만드는"</strong> 개발자입니다.<br>
      사용자가 겪는 불편함을 기술로 해결하는 것에 가치를 두고,<br>
      직접 기획부터 배포까지 경험하며 성장하고 있습니다.
    </p>
    <div class="hero-keywords">
      <span class="keyword-badge">🔧 풀스택 경험</span>
      <span class="keyword-badge">☁️ AWS 인프라</span>
      <span class="keyword-badge">🚀 사이드 프로젝트</span>
    </div>
    <div class="hero-cta">
      <a href="mailto:momo990305@gmail.com" class="cta-btn cta-primary">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect width="20" height="16" x="2" y="4" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>
        연락하기
      </a>
      <a href="https://github.com/Hoooon22" class="cta-btn cta-secondary">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
        GitHub
      </a>
      <a href="https://devzip.site" class="cta-btn cta-secondary">
        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"/><path d="M12 4v1.5M18 6l-1.1 1.1M20 12h-1.5M18 18l-1.1-1.1M12 20v-1.5M6 18l1.1-1.1M4 12h1.5M6 6l1.1 1.1"/></svg>
        DevZip
      </a>
    </div>
  </div>
</div>

<!-- 핵심 역량 섹션 -->
<div class="section">
  <div class="section-header">
    <div class="section-icon">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>
    </div>
    <h2 class="section-title">핵심 역량</h2>
  </div>

  <div class="competency-grid">
    <div class="competency-card">
      <div class="competency-icon">🏗️</div>
      <h3 class="competency-title">풀스택 개발 경험</h3>
      <p class="competency-desc">
        프론트엔드(React, Next.js)부터 백엔드(Spring Boot, Node.js), 데이터베이스(MySQL)까지 전 영역을 경험했습니다. 서비스 전체를 이해하고 협업할 수 있습니다.
      </p>
    </div>

    <div class="competency-card">
      <div class="competency-icon">☁️</div>
      <h3 class="competency-title">AWS 클라우드 인프라</h3>
      <p class="competency-desc">
        EC2, RDS, S3, Route53 등을 활용해 직접 서비스를 배포하고 운영했습니다. 비용 최적화와 서버 관리 경험을 보유하고 있습니다.
      </p>
    </div>

    <div class="competency-card">
      <div class="competency-icon">🎯</div>
      <h3 class="competency-title">문제 해결 중심 개발</h3>
      <p class="competency-desc">
        실제 사용자의 불편함을 발견하고 해결하는 것을 좋아합니다. DevZip, 퐁당 등 직접 기획하고 운영하는 서비스를 통해 이를 실천하고 있습니다.
      </p>
    </div>
  </div>
</div>

<!-- 대표 프로젝트 섹션 -->
<div class="section">
  <div class="section-header">
    <div class="section-icon">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2z"/></svg>
    </div>
    <h2 class="section-title">대표 프로젝트</h2>
  </div>

  <!-- DevZip 프로젝트 -->
  <div class="featured-project">
    <div class="project-banner" style="background: linear-gradient(to right, #2563eb, #0ea5e9);"></div>
    <div class="project-content">
      <div class="project-visual">
        <span class="project-badge">운영 중</span>
        <img src="assets/images/devzip/mainpage_new.png" alt="DevZip 메인 페이지">
      </div>
      <div class="project-info">
        <h3>DevZip - 개발 프로젝트 플랫폼</h3>
        <p class="project-period">2024.01 ~ 현재 (개인 프로젝트)</p>
        <p class="project-summary">
          다양한 실험적 아이디어와 실서비스를 한곳에 모아놓은 <strong>개인 개발 플랫폼</strong>입니다.
          실시간 채팅, 방명록, 트렌드 분석 등 다양한 기능을 직접 구현하고 운영하고 있습니다.
        </p>
        <div class="project-highlight">
          <h4>이 프로젝트를 통해 ...</h4>
          <p>
            기획 → 개발 → 배포 → 운영까지 전 과정을 혼자 수행하며,<br>
            <strong>실제 서비스를 만들고 유지하는 역량</strong>을 갖추었습니다.
          </p>
        </div>
        <div class="live-services">
          <h4 class="live-services-title">운영 중인 서비스</h4>
          <div class="service-list">
            <a href="https://www.devzip.site/commandstack" class="service-item">
              <div class="service-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="4 17 10 11 4 5"/><line x1="12" y1="19" x2="20" y2="19"/></svg>
              </div>
              <div class="service-info">
                <div class="service-name">Command Stack</div>
                <p class="service-desc">터미널 스타일의 개발자용 스케줄러 - 할 일을 명령어처럼 관리</p>
              </div>
            </a>
            <a href="https://www.devzip.site/conflux" class="service-item">
              <div class="service-icon">
                <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><path d="M12 2a14.5 14.5 0 0 0 0 20 14.5 14.5 0 0 0 0-20"/><path d="M2 12h20"/></svg>
              </div>
              <div class="service-info">
                <div class="service-name">Conflux</div>
                <p class="service-desc">통합 알림 관제 센터 - 흩어진 개발 도구 알림을 하나로</p>
              </div>
            </a>
          </div>
        </div>
        <div class="tech-stack">
          <span class="tech-tag">Next.js</span>
          <span class="tech-tag">React</span>
          <span class="tech-tag">Node.js</span>
          <span class="tech-tag">MySQL</span>
          <span class="tech-tag">AWS</span>
        </div>
        <div class="project-links">
          <a href="https://devzip.site" class="project-link link-primary">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 13v6a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h6"/><polyline points="15 3 21 3 21 9"/><line x1="10" y1="14" x2="21" y2="3"/></svg>
            사이트 방문
          </a>
          <a href="https://github.com/Hoooon22/devzip" class="project-link link-secondary">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
            GitHub
          </a>
          <a href="docs/projects/devzip/devzip" class="project-link link-secondary">상세 보기</a>
        </div>
      </div>
    </div>
  </div>

  <!-- 퐁당 프로젝트 -->
  <div class="featured-project">
    <div class="project-banner" style="background: linear-gradient(to right, #10b981, #059669);"></div>
    <div class="project-content">
      <div class="project-visual">
        <span class="project-badge">서비스 종료</span>
        <img src="assets/images/pongdang/1_퐁당로고.png" alt="퐁당 매거진">
      </div>
      <div class="project-info">
        <h3>퐁당 매거진 - 청소년 진로 웹매거진</h3>
        <p class="project-period">2022.06 ~ 2023.06 (팀 프로젝트)</p>
        <p class="project-summary">
          청소년에게 다양한 직업을 소개하는 <strong>웹매거진 서비스</strong>의 풀스택 개발을 담당했습니다.
          실제 사용자를 대상으로 서비스를 운영하며 피드백을 반영하는 경험을 했습니다.
        </p>
        <div class="project-highlight">
          <h4>이 프로젝트를 통해 ...</h4>
          <p>
            비개발자 팀원과 협업하며 <strong>요구사항 분석 → 설계 → 구현</strong> 과정을 경험했고,<br>
            실서비스 배포와 운영을 통해 <strong>책임감 있는 개발</strong>을 배웠습니다.
          </p>
        </div>
        <div class="tech-stack">
          <span class="tech-tag">Spring Boot</span>
          <span class="tech-tag">React</span>
          <span class="tech-tag">Node.js</span>
          <span class="tech-tag">MySQL</span>
          <span class="tech-tag">AWS</span>
        </div>
        <div class="project-links">
          <a href="https://github.com/Hoooon22/Pongdang_Server2" class="project-link link-secondary">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
            GitHub
          </a>
          <a href="docs/projects/pongdang/pongdang" class="project-link link-secondary">상세 보기</a>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- 그 외 프로젝트 -->
<div class="section">
  <div class="section-header">
    <div class="section-icon">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect width="7" height="7" x="3" y="3" rx="1"/><rect width="7" height="7" x="14" y="3" rx="1"/><rect width="7" height="7" x="14" y="14" rx="1"/><rect width="7" height="7" x="3" y="14" rx="1"/></svg>
    </div>
    <h2 class="section-title">그 외 프로젝트</h2>
  </div>

  <div class="other-projects-grid">
    <div class="mini-project-card">
      <img src="assets/images/gameadvisor/bloons-td6-analysis-test.png" alt="GameAdvisor" class="mini-project-image">
      <div class="mini-project-header">
        <h4 class="mini-project-title">GameAdvisor</h4>
        <span class="mini-project-year">2025 (개발중)</span>
      </div>
      <p class="mini-project-desc">게임 화면을 실시간 분석하여 최적의 전략을 제안하는 데스크톱 애플리케이션</p>
      <div class="mini-tech-stack">
        <span class="mini-tech">Spring Boot</span>
        <span class="mini-tech">JavaFX</span>
        <span class="mini-tech">OpenCV</span>
      </div>
      <div class="mini-project-links">
        <a href="docs/projects/GameAdvisor/GameAdvisor" class="mini-link">상세 보기</a>
        <a href="https://github.com/Hoooon22/GameAdvisor" class="mini-link">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </a>
      </div>
    </div>

    <div class="mini-project-card">
      <img src="assets/images/profile/스크린샷 2023-03-01 오후 2.40.40.png" alt="어린이집 CCTV 영상처리" class="mini-project-image">
      <div class="mini-project-header">
        <h4 class="mini-project-title">어린이집 CCTV 영상처리</h4>
        <span class="mini-project-year">2022</span>
      </div>
      <p class="mini-project-desc">아동학대 방지를 위한 CCTV 영상 분석 및 효율적 반출 시스템 (졸업 프로젝트)</p>
      <div class="mini-tech-stack">
        <span class="mini-tech">Python</span>
        <span class="mini-tech">OpenCV</span>
        <span class="mini-tech">React</span>
      </div>
      <div class="mini-project-links">
        <a href="https://github.com/CSID-DGU/2022-2-CECD4-STEPBACK-1" class="mini-link">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </a>
      </div>
    </div>

    <div class="mini-project-card">
      <div class="mini-project-images">
        <img src="assets/images/profile/스크린샷 2022-10-28 오후 7.36.11.png" alt="VR 화학실험실 1">
        <img src="assets/images/profile/스크린샷 2022-10-28 오후 7.36.22.png" alt="VR 화학실험실 2">
      </div>
      <div class="mini-project-header">
        <h4 class="mini-project-title">VR 화학실험실</h4>
        <span class="mini-project-year">2022</span>
      </div>
      <p class="mini-project-desc">안전사고 예방과 과학 교육을 위한 VR 가상 실험실 환경</p>
      <div class="mini-tech-stack">
        <span class="mini-tech">Unity</span>
        <span class="mini-tech">C#</span>
        <span class="mini-tech">Blender</span>
      </div>
      <div class="mini-project-links">
        <a href="https://github.com/Hoooon22/ChemicalLab" class="mini-link">
          <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </a>
      </div>
    </div>

    <div class="mini-project-card">
      <div class="mini-project-images">
        <img src="assets/images/profile/스크린샷 2025-01-07 오후 4.07.56.png" alt="GitHub Summary Extension 1">
        <img src="assets/images/profile/스크린샷 2025-01-07 오후 4.08.28.png" alt="GitHub Summary Extension 2">
      </div>
      <div class="mini-project-header">
        <h4 class="mini-project-title">GitHub Summary Extension</h4>
        <span class="mini-project-year">2024</span>
      </div>
      <p class="mini-project-desc">OpenAI API를 활용해 GitHub 레포지토리를 자동 요약하는 Chrome Extension</p>
      <div class="mini-tech-stack">
        <span class="mini-tech">JavaScript</span>
        <span class="mini-tech">OpenAI API</span>
      </div>
    </div>
  </div>
</div>

<!-- 기술 스택 -->
<div class="section">
  <div class="section-header">
    <div class="section-icon">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>
    </div>
    <h2 class="section-title">기술 스택</h2>
  </div>

  <div class="skills-container">
    <div class="skill-category">
      <h4 class="skill-category-title">💻 Backend</h4>
      <div class="skill-list">
        <span class="skill-item">Java</span>
        <span class="skill-item">Spring Boot</span>
        <span class="skill-item">Node.js</span>
      </div>
    </div>

    <div class="skill-category">
      <h4 class="skill-category-title">🎨 Frontend</h4>
      <div class="skill-list">
        <span class="skill-item">React</span>
        <span class="skill-item">Next.js</span>
        <span class="skill-item">JavaScript</span>
      </div>
    </div>

    <div class="skill-category">
      <h4 class="skill-category-title">🗃️ Database</h4>
      <div class="skill-list">
        <span class="skill-item">MySQL</span>
      </div>
    </div>

    <div class="skill-category">
      <h4 class="skill-category-title">☁️ Infra</h4>
      <div class="skill-list">
        <span class="skill-item">AWS</span>
        <span class="skill-item">Linux</span>
        <span class="skill-item">Git</span>
      </div>
    </div>
  </div>
</div>

<!-- 학력 및 경험 -->
<div class="section">
  <div class="section-header">
    <div class="section-icon">
      <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M22 10v6M2 10l10-5 10 5-10 5z"/><path d="M6 12v5c3 3 9 3 12 0v-5"/></svg>
    </div>
    <h2 class="section-title">학력 및 경험</h2>
  </div>

  <div class="competency-grid">
    <div class="competency-card">
      <div class="competency-icon">🎓</div>
      <h3 class="competency-title">동국대학교 컴퓨터공학과</h3>
      <p class="competency-desc">
        2018.03 ~ 2023.02 졸업<br>
        전공 교과목을 통해 자료구조, 알고리즘, 운영체제, 데이터베이스 등 CS 기초를 탄탄히 다졌습니다.
      </p>
    </div>

    <div class="competency-card">
      <div class="competency-icon">🔬</div>
      <h3 class="competency-title">인간-로봇 상호작용 연구실</h3>
      <p class="competency-desc">
        2019.07 ~ 2021.04 학부연구생<br>
        시각/청각 장애인을 위한 접근성 연구에 참여하며, 사회적 가치를 담은 기술 개발을 경험했습니다.
      </p>
    </div>
  </div>
</div>

<!-- 연락처 섹션 -->
<div class="contact-section">
  <h2 class="contact-title">문제의 본질을 파악하고 해결하는 개발자</h2>
  <p class="contact-subtitle">언제든 편하게 연락 주세요!</p>
  <div class="contact-links">
    <a href="mailto:momo990305@gmail.com" class="contact-link">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect width="20" height="16" x="2" y="4" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>
      momo990305@gmail.com
    </a>
    <a href="https://github.com/Hoooon22" class="contact-link">
      <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
      GitHub
    </a>
  </div>
</div>
