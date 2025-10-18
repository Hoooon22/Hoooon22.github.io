---
layout: default
title: Hoooon22's Log
nav_order: 1
description: "Hoooon22 is logging..."
permalink: /
---

<!-- 스크립트를 페이지 상단에 배치 -->
<script>
// 팝오버 관련 변수
let activePopover = null;

// 팝오버 열기 함수
function toggleCustomPopover(popoverId, button) {
  console.log("toggleCustomPopover 호출됨", popoverId);
  
  // 이미 열린 팝오버가 있으면 닫기
  if (activePopover) {
    closePopover(activePopover);
  }
  
  const popover = document.getElementById(popoverId);
  if (!popover) {
    console.error("Popover not found:", popoverId);
    return;
  }
  
  // 버튼 위치 기준으로 팝오버 위치 설정
  const buttonRect = button.getBoundingClientRect();
  const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
  
  // 팝오버 위치 설정 (버튼 아래에 표시)
  popover.style.top = (buttonRect.bottom + scrollTop + 10) + 'px';
  popover.style.left = buttonRect.left + 'px';
  
  // 팝오버가 화면 오른쪽 경계를 벗어나지 않도록 조정
  setTimeout(() => {
    const popoverRect = popover.getBoundingClientRect();
    const windowWidth = window.innerWidth;
    
    if (popoverRect.right > windowWidth) {
      popover.style.left = (windowWidth - popoverRect.width - 20) + 'px';
    }
  }, 0);
  
  // 팝오버 표시
  popover.classList.add('show');
  activePopover = popover;
  
  // 클릭 이벤트 리스너 추가 (팝오버 외부 클릭 시 닫기)
  setTimeout(() => {
    document.addEventListener('click', documentClickHandler);
  }, 10);
  
  console.log("Popover opened:", popoverId);
}

// 팝오버 닫기 함수
function closePopover(popover) {
  if (!popover) return;
  
  popover.classList.remove('show');
  activePopover = null;
  
  // 클릭 이벤트 리스너 제거
  document.removeEventListener('click', documentClickHandler);
  
  console.log("Popover closed");
}

// 문서 클릭 이벤트 핸들러 (팝오버 외부 클릭 시 닫기)
function documentClickHandler(e) {
  if (activePopover) {
    const isClickInside = activePopover.contains(e.target) || 
                         e.target.classList.contains('popover-btn') || 
                         e.target.hasAttribute('data-popover') || 
                         (e.target.tagName === 'BUTTON' && e.target.getAttribute('onclick') && e.target.getAttribute('onclick').includes('toggleCustomPopover'));
    
    if (!isClickInside) {
      closePopover(activePopover);
    }
  }
}

// 모달 열기 함수 (기존 모달용)
function openModal(modalId) {
  console.log("Opening modal:", modalId);
  const modal = document.getElementById(modalId);
  if (!modal) {
    console.error("Modal not found:", modalId);
    return;
  }
  
  // 모달 표시
  modal.classList.add('show');
  
  // 배경 스크롤 방지
  document.body.style.overflow = 'hidden';
  
  console.log("Modal opened:", modalId);
}

// 모달 닫기 함수
function closeModal(modal) {
  console.log("Closing modal");
  modal.classList.remove('show');
  
  // 배경 스크롤 다시 활성화
  document.body.style.overflow = '';
}
</script>

<style>
details summary {
  list-style: none;
}
details summary::-webkit-details-marker {
  display: none;
}
</style>

<h1 style="color:black; margin-top: 0; font-weight:bold; font-size: 3rem;">Hoooon22</h1>
{: .fs-9 }

<span style="font-size: 1.5rem; background: linear-gradient(to right, #4776E6, #8E54E9); -webkit-background-clip: text; -webkit-text-fill-color: transparent;">Web & Server Developer</span>
{: .fs-4 .fw-300 }

---
<h1 style="color:#2c3e50; margin-top: -2%; font-weight:bold; padding-bottom: 10px; border-bottom: 2px solid #3498db;">Profile</h1>

<div style="display: flex; justify-content: space-around; flex-wrap: wrap; gap: 20px;">
    <div style="width: 45%; min-width: 300px;">
        <img src="../../../../assets/images/IMG_0675.JPG" alt="It's me!" style="width: 90%; border-radius: 15px; box-shadow: 0 4px 8px rgba(0,0,0,0.1);">
    </div>
    <div style="width: 55%; min-width: 300px;">
        <h2 style="margin-top: 0%; color: #3498db;"><strong>김지훈</strong></h2>
        <p style="font-size: 1.2rem; color: #7f8c8d;">웹 & 서버 개발자</p>

        <h3 style="color: #2c3e50; border-left: 4px solid #3498db; padding-left: 10px;">학력</h3>
        <ul style="list-style-type: none; padding-left: 0;">
            <li style="margin-bottom: 5px; padding: 5px 0;">
                <span style="background-color: #f8f9fa; padding: 5px 10px; border-radius: 5px; margin-right: 10px;">🎓</span>
                동국대학교 컴퓨터공학과 (2018.03 ~ 2023.02)
            </li>
        </ul>

        <h3 style="color: #2c3e50; border-left: 4px solid #3498db; padding-left: 10px;">기타</h3>
        <ul style="list-style-type: none; padding-left: 0;">
            <li style="margin-bottom: 5px; padding: 5px 0;">
                <span style="background-color: #f8f9fa; padding: 5px 10px; border-radius: 5px; margin-right: 10px;">🔬</span>
                동국대학교 인간-로봇 상호작용 연구실 학부연구생 (2019.07 ~ 2021.04)
            </li>
        </ul>

        <!-- <h3>경력</h3>
        <ul>
        </ul> -->

       <!-- 이미지 뱃지 링크의 'link' 파라미터는 작동하지 않으므로 'url' 파라미터로 변경해야 합니다 -->
       <!-- 또한 HTML 태그에서는 이미지와 링크를 분리하여 적용해야 합니다 -->
        
       <!-- Tech Blog Badge -->
       <!-- Notion Badge -->
       <!-- Gmail Badge -->

    </div>
</div>

<div style="display: flex; justify-content: center; margin-top: 30px; gap: 15px; flex-wrap: wrap;">
    <a href="https://hoooon22.github.io/" style="text-decoration: none;">
        <div style="background-color: #2c3e50; color: white; padding: 10px 15px; border-radius: 10px; display: flex; align-items: center; gap: 8px; transition: transform 0.3s ease;">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
            Tech Blog
        </div>
    </a>
    <a href="mailto:momo990305@gmail.com" style="text-decoration: none;">
        <div style="background-color: #d14836; color: white; padding: 10px 15px; border-radius: 10px; display: flex; align-items: center; gap: 8px; transition: transform 0.3s ease;">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="16" x="2" y="4" rx="2"/><path d="m22 7-8.97 5.7a1.94 1.94 0 0 1-2.06 0L2 7"/></svg>
            Gmail
        </div>
    </a>
    <a href="https://devzip.cloud" style="text-decoration: none;">
        <div style="background-color: #0077b5; color: white; padding: 10px 15px; border-radius: 10px; display: flex; align-items: center; gap: 8px; transition: transform 0.3s ease;">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 12a3 3 0 1 1-6 0 3 3 0 0 1 6 0Z"/><path d="M12 4v1.5M18 6l-1.1 1.1M20 12h-1.5M18 18l-1.1-1.1M12 20v-1.5M6 18l1.1-1.1M4 12h1.5M6 6l1.1 1.1"/></svg>
            개발 프로젝트 모음집 - DevZip
        </div>
    </a>
</div>

---
<h1 style="color:#2c3e50; margin-top: -2%; font-weight:bold; padding-bottom: 10px; border-bottom: 2px solid #3498db;">Tech Stack</h1>

<div style="background-color: #f8f9fa; border-radius: 15px; padding: 20px; box-shadow: 0 4px 8px rgba(0,0,0,0.05);">
    <div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 15px;">
        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">💻</span>Programming Languages
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">Java</li>
                <li style="padding: 5px 0;">C/C++</li>
            </ul>
        </div>
        
        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">🛠️</span>Frameworks
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">SpringBoot</li>
                <li style="padding: 5px 0;">Node.js</li>
                <li style="padding: 5px 0;">React</li>
            </ul>
        </div>

        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">🌐</span>Web Technologies
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">HTML5</li>
                <li style="padding: 5px 0;">CSS</li>
                <li style="padding: 5px 0;">Javascript</li>
                <li style="padding: 5px 0;">ASP</li>
            </ul>
        </div>

        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">🗃️</span>Databases
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">MySQL</li>
            </ul>
        </div>

        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">🔄</span>Version Control
            </h3>
    <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">Git</li>
    </ul>
</div>

        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">☁️</span>Cloud Services
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">AWS</li>
            </ul>
        </div>

        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">💿</span>Operating Systems
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">Linux</li>
            </ul>
        </div>

        <div style="background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.05);">
            <h3 style="color: #3498db; margin-top: 0; border-bottom: 1px solid #ecf0f1; padding-bottom: 8px;">
                <span style="margin-right: 8px;">🎮</span>Miscellaneous
            </h3>
            <ul style="list-style-type: none; padding-left: 0;">
                <li style="padding: 5px 0;">Unity</li>
            </ul>
        </div>
    </div>
</div>

---
<h1 style="color:#2c3e50; margin-top: -2%; font-weight:bold; padding-bottom: 10px; border-bottom: 2px solid #3498db;">Projects</h1>

<div class="projects-container" style="display: grid; grid-template-columns: 1fr; gap: 25px; margin-top: 30px;">

<!-- DevZip 프로젝트 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #0077b5, #00c6ff); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">DEV ZIP - 실험적 아이디어와 실서비스 프로젝트 쇼케이스</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2024-현재</div>
      <div style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">웹 서비스</div>
    </div>
    <div style="display: flex; justify-content: center; margin: 15px 0;">
      <img src="../../../../assets/images/devzip/mainpage.png" alt="DEV ZIP" style="max-width: 80%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
        <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">
      다양한 실험적 아이디어와 실서비스 프로젝트를 한곳에 모아놓은 플랫폼입니다. 방명록, 농담 API, 물리 퀴즈 등 재미있는 실험부터 트레이스보드, 트렌드챗 같은 실용적인 서비스까지 다양한 프로젝트를 선보입니다.
      <br><br>
      <strong>주요 기능:</strong>
      <ul style="list-style-type: disc; padding-left: 20px;">
        <li><a href="https://devzip.cloud/livechat" target="_blank">실시간 채팅</a></li>
        <li><a href="https://devzip.cloud/Guestbook" target="_blank">방명록</a></li>
        <li><a href="https://devzip.cloud/Joke" target="_blank">농담</a></li>
        <li><a href="https://devzip.cloud/apiPage" target="_blank">API 문서</a></li>
        <li><a href="https://devzip.cloud/dashboard" target="_blank">대시보드</a> (관리자)</li>
        <li><a href="https://devzip.cloud/traceboard" target="_blank">트레이스보드</a> (관리자)</li>
        <li><a href="https://devzip.cloud/trendchat" target="_blank">트렌드챗</a></li>
        <li><a href="https://devzip.cloud/physics-quiz" target="_blank">물리 퀴즈</a></li>
      </ul>
    </p>
    
    <div style="margin-top: 10px; margin-bottom: 15px;">
      <h4 style="color: #0077b5; font-size: 1rem; margin-bottom: 10px; border-left: 3px solid #0077b5; padding-left: 10px;">DevZip 서비스</h4>
      <div style="display: flex; flex-wrap: wrap; gap: 8px;">
        <a href="https://devzip.cloud/traceboard" style="text-decoration: none; display: inline-block; background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem; transition: background-color 0.2s ease;">
          <span style="display: flex; align-items: center; gap: 5px;">
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M2 12s3-7 10-7 10 7 10 7-3 7-10 7-10-7-10-7Z"></path><circle cx="12" cy="12" r="3"></circle></svg>
            트레이스보드
          </span>
        </a>
        <a href="https://devzip.cloud/trendchat" style="text-decoration: none; display: inline-block; background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem; transition: background-color 0.2s ease;">
          <span style="display: flex; align-items: center; gap: 5px;">
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 7 13.5 15.5 8.5 10.5 2 17"></polyline><polyline points="16 7 22 7 22 13"></polyline></svg>
            트렌드챗
          </span>
        </a>
        <a href="https://devzip.cloud/dashboard" style="text-decoration: none; display: inline-block; background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem; transition: background-color 0.2s ease;">
          <span style="display: flex; align-items: center; gap: 5px;">
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="18" height="18" x="3" y="3" rx="2" ry="2"></rect><line x1="3" x2="21" y1="9" y2="9"></line><line x1="9" x2="9" y1="21" y2="9"></line></svg>
            대시보드
          </span>
        </a>
        <a href="https://devzip.cloud/apiPage" style="text-decoration: none; display: inline-block; background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem; transition: background-color 0.2s ease;">
          <span style="display: flex; align-items: center; gap: 5px;">
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M20 14.66V20a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h5.34"></path><polygon points="18 2 22 6 12 16 8 16 8 12 18 2"></polygon></svg>
            API 문서
          </span>
        </a>
        <a href="https://devzip.cloud/Guestbook" style="text-decoration: none; display: inline-block; background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem; transition: background-color 0.2s ease;">
          <span style="display: flex; align-items: center; gap: 5px;">
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 12c2.76 0 5-2.24 5-5s-2.24-5-5-5-5 2.24-5 5 2.24 5 5 5Z"></path><path d="M19 21v-2a7 7 0 0 0-14 0v2"></path></svg>
            방명록
          </span>
        </a>
        <a href="https://devzip.cloud/Joke" style="text-decoration: none; display: inline-block; background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem; transition: background-color 0.2s ease;">
          <span style="display: flex; align-items: center; gap: 5px;">
            <svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"></circle><path d="M8 14s1.5 2 4 2 4-2 4-2"></path><line x1="9" x2="9.01" y1="9" y2="9"></line><line x1="15" x2="15.01" y1="9" y2="9"></line></svg>
            농담
          </span>
        </a>
      </div>
    </div>
    
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Next.js</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">React</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Node.js</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">MongoDB</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">AWS</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px; flex-wrap: wrap;">
      <a href="https://hoooon22.github.io/docs/projects/devzip/devzip" style="text-decoration: none; border: none; display: inline-block; background-color: #3498db; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">프로젝트 상세</a>
      <a href="https://devzip.cloud" style="text-decoration: none; border: none; display: inline-block; background-color: #2980b9; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">사이트 방문</a>
      <span style="color: #e74c3c; font-size: 0.9rem; margin-left: 8px;">AWS(※ 현재 서버 비용 문제로 서비스가 일시 중단) -> **Local 서버 서비스 중**</span>
      <a href="https://github.com/Hoooon22/devzip" style="text-decoration: none; border: none; display: inline-block; background-color: #2c3e50; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </span>
      </a>
    </div>
  </div>
</div>

<!-- project 1 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #3498db, #2980b9); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">퐁당 매거진 웹사이트 제작</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #f0f4f8; color: #3498db; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2022-2023</div>
      <div style="background-color: #f0f4f8; color: #3498db; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">풀스택 개발</div>
    </div>
    <div style="display: flex; justify-content: center; margin: 15px 0;">
        <a href="https://stoneinwell.com/">
        <img src="../../../../assets/images/pongdang/1_퐁당로고.png" alt="퐁당 사이" style="max-width: 70%; border-radius: 10px; transition: transform 0.3s ease;">
        </a>
</div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">청소년들에게 세상에 있는 다양한 직업들을 소개해주는 웹매거진 '매거진 퐁당'의 풀스택 개발을 맡았습니다.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #e3f2fd; color: #3498db; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">AWS</span>
      <span style="background-color: #e3f2fd; color: #3498db; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">HTML/CSS/JS</span>
      <span style="background-color: #e3f2fd; color: #3498db; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Node.js</span>
      <span style="background-color: #e3f2fd; color: #3498db; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">React</span>
      <span style="background-color: #e3f2fd; color: #3498db; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">SpringBoot</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px;">
      <button onclick="window.location.href='https://hoooon22.github.io/docs/projects/pongdang/pongdang/';" style="text-decoration: none; border: none; display: inline-block; background-color: #3498db; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">프로젝트 상세</button>
      <button onclick="window.location.href='https://github.com/Hoooon22/Pongdang_Server2';" style="text-decoration: none; border: none; display: inline-block; background-color: #2c3e50; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </span>
      </button>
      <button onclick="window.location.href='https://www.instagram.com/mz.pongdang/';" style="text-decoration: none; border: none; display: inline-block; background-color: #E4405F; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect width="20" height="20" x="2" y="2" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" x2="17.51" y1="6.5" y2="6.5"/></svg>
          Instagram
        </span>
      </button>
    </div>
</div>
</div>

<!-- GameAdvisor 프로젝트 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #2ecc71, #27ae60); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">GameAdvisor - 게임 화면 분석 어시스턴트</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2025-현재</div>
      <div style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">데스크톱 앱</div>
      <div style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">개발중</div>
    </div>
    <div style="display: flex; justify-content: center; margin: 15px 0;">
      <img src="../../../../assets/images/gameadvisor/bloons-td6-analysis-test.png" alt="GameAdvisor 화면 분석" style="max-width: 80%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">게임 화면을 실시간으로 분석하여 플레이어에게 최적의 전략과 조언을 제공하는 데스크톱 어플리케이션입니다. Spring Boot 백엔드와 JavaFX 클라이언트로 구현되었습니다.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Spring Boot</span>
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">JavaFX</span>
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">OpenCV</span>
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Deep Learning</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px;">
      <button onclick="window.location.href='https://hoooon22.github.io/docs/projects/GameAdvisor/GameAdvisor/';" style="text-decoration: none; border: none; display: inline-block; background-color: #27ae60; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">프로젝트 상세</button>
      <button onclick="window.location.href='https://github.com/Hoooon22/GameAdvisor';" style="text-decoration: none; border: none; display: inline-block; background-color: #2c3e50; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </span>
      </button>
    </div>
  </div>
</div>

<!-- project 2 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #e74c3c, #c0392b); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">어린이집 CCTV 영상처리 시스템</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #fdf2f0; color: #e74c3c; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2022</div>
      <div style="background-color: #fdf2f0; color: #e74c3c; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">영상처리</div>
    </div>
    <div style="display: flex; justify-content: center; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2023-03-01 오후 2.40.40.png" alt="" style="max-width: 80%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">아동학대 방지를 위해 어린이집 내 CCTV 영상을 효율적으로 반출하는 시스템 개발. 학대 의심 구간 탐지 및 프라이버시 보호를 위한 영상처리 기능 구현.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #fef5f5; color: #e74c3c; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">영상처리</span>
      <span style="background-color: #fef5f5; color: #e74c3c; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Front-end</span>
      <span style="background-color: #fef5f5; color: #e74c3c; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Back-end</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px; flex-wrap: wrap;">
      <button onclick="window.location.href='https://github.com/CSID-DGU/2022-2-CECD4-STEPBACK-1';" style="text-decoration: none; border: none; display: inline-block; background-color: #2c3e50; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </span>
      </button>
    </div>
</div>
</div>

<!-- project 3 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #f39c12, #d35400); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">동국대학교 전자불전문화콘텐츠연구소 아카이브</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #fdf6e9; color: #f39c12; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2020</div>
      <div style="background-color: #fdf6e9; color: #f39c12; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">웹개발</div>
    </div>
    <div style="display: flex; justify-content: center; gap: 10px; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.21.03.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.21.25.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">동국대학교 전자불전문화콘텐츠연구소의 불교문화가 담긴 사진 등의 빅데이터들을 저장하고 열람할 수 있는 홈페이지 제작.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #fef6e7; color: #f39c12; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">HTML/CSS/JS</span>
      <span style="background-color: #fef6e7; color: #f39c12; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Node.js</span>
      <span style="background-color: #fef6e7; color: #f39c12; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">MySQL</span>
    </div>
  </div>
</div>

<!-- project 4 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #9b59b6, #8e44ad); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">안전사고 예방과 과학 교육을 위한 VR실험실</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #f4ecf7; color: #9b59b6; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2022</div>
      <div style="background-color: #f4ecf7; color: #9b59b6; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">VR 개발</div>
    </div>
    <div style="display: flex; justify-content: center; gap: 10px; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.36.11.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.36.22.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">실제 화학 실험에서의 위험사고와 경제적 손실을 최소화하기 위한 VR 가상 실험실 환경 구현.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #f5eef8; color: #9b59b6; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Unity</span>
      <span style="background-color: #f5eef8; color: #9b59b6; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">C#</span>
      <span style="background-color: #f5eef8; color: #9b59b6; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Blender</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px; flex-wrap: wrap;">
      <button onclick="window.location.href='https://github.com/Hoooon22/ChemicalLab';" style="text-decoration: none; border: none; display: inline-block; background-color: #2c3e50; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
          GitHub
        </span>
      </button>
    </div>
</div>
</div>

<!-- project 5 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #27ae60, #2ecc71); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">동국대학교 C언어 프로그래밍 교안 제작</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #eafaf1; color: #27ae60; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2019-2020</div>
      <div style="background-color: #eafaf1; color: #27ae60; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">교육자료</div>
    </div>
    <div style="display: flex; justify-content: center; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.28.28.png" alt="" style="max-width: 70%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">동국대학교의 이공계 학생들을 위한 문제풀이 중심의 C언어 프로그래밍 교안 제작. Project1-주기율표 계산 프로그램 구현.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">C언어</span>
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">프로그래밍 기초</span>
      <span style="background-color: #e8f8f5; color: #27ae60; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">교육</span>
    </div>
  </div>
</div>

<!-- project 6 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #16a085, #1abc9c); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">시각장애인을 위한 스마트 점자 패널</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #e8f6f3; color: #16a085; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2019</div>
      <div style="background-color: #e8f6f3; color: #16a085; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">연구</div>
    </div>
    <div style="display: flex; justify-content: center; gap: 10px; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.22.58.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.23.25.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">시각장애인의 스마트폰을 통한 정보접근성 향상을 위한 '스마트 점자 패널' 설계. 스마트폰 음성이 아닌 점자를 이용한 정보 전달 방식.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #e8f6f3; color: #16a085; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">접근성</span>
      <span style="background-color: #e8f6f3; color: #16a085; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">연구 논문</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px; flex-wrap: wrap;">
      <button onclick="window.location.href='../../../../assets/files/김지훈_한국지능시스템학회논문.pdf';" style="text-decoration: none; border: none; display: inline-block; background-color: #2980b9; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path><polyline points="14 2 14 8 20 8"></polyline><line x1="16" y1="13" x2="8" y2="13"></line><line x1="16" y1="17" x2="8" y2="17"></line><line x1="10" y1="9" x2="8" y2="9"></line></svg>
          논문 보기
        </span>
      </button>
    </div>
  </div>
</div>

<!-- project 7 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #2980b9, #3498db); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">스마트미러 청각장애인 구화훈련 앱</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #ebf5fb; color: #2980b9; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2020-2021</div>
      <div style="background-color: #ebf5fb; color: #2980b9; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">앱 개발</div>
    </div>
    <div style="display: flex; justify-content: center; gap: 10px; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.26.04.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
      <img src="../../../../assets/images/profile/스크린샷 2022-10-28 오후 7.26.25.png" alt="" style="max-width: 45%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">스마트미러를 활용한 청각장애인 구화훈련 애플리케이션 개발. STT(Speech to Text) 알고리즘 기반 발음 교정 시스템.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #ebf5fb; color: #2980b9; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Android Studio</span>
      <span style="background-color: #ebf5fb; color: #2980b9; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">STT</span>
      <span style="background-color: #ebf5fb; color: #2980b9; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">접근성</span>
    </div>
    <div style="margin-top: 20px; display: flex; gap: 10px; flex-wrap: wrap;">
      <button onclick="window.location.href='../../../../assets/files/김지훈_한국지능시스템학회논문.pdf';" style="text-decoration: none; border: none; display: inline-block; background-color: #2980b9; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">
        <span style="display: flex; align-items: center; gap: 5px;">
          <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path><polyline points="14 2 14 8 20 8"></polyline><line x1="16" y1="13" x2="8" y2="13"></line><line x1="16" y1="17" x2="8" y2="17"></line><line x1="10" y1="9" x2="8" y2="9"></line></svg>
          논문 보기
        </span>
      </button>
    </div>
  </div>
</div>

<!-- project 8 -->
<div class="project-card" style="width: 100%; background: white; border-radius: 15px; overflow: hidden; box-shadow: 0 5px 15px rgba(0,0,0,0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; position: relative;">
  <div style="height: 10px; background: linear-gradient(to right, #8e44ad, #9b59b6); width: 100%;"></div>
  <div style="padding: 20px;">
    <h3 style="color: #2c3e50; margin-top: 0; font-size: 1.3rem;">Chrome Extension 개발 - Github_Summary</h3>
    <div style="display: flex; margin: 15px 0;">
      <div style="background-color: #f4ecf7; color: #8e44ad; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem; margin-right: 10px;">2024-현재</div>
      <div style="background-color: #f4ecf7; color: #8e44ad; padding: 5px 10px; border-radius: 20px; font-size: 0.8rem;">브라우저 확장</div>
    </div>
    <div style="display: flex; justify-content: center; gap: 10px; margin: 15px 0;">
      <img src="../../../../assets/images/profile/스크린샷 2025-01-07 오후 4.07.56.png" alt="" style="max-width: 65%; border-radius: 10px; transition: transform 0.3s ease;">
      <img src="../../../../assets/images/profile/스크린샷 2025-01-07 오후 4.08.28.png" alt="" style="max-width: 25%; border-radius: 10px; transition: transform 0.3s ease;">
    </div>
    <p style="color: #7f8c8d; font-size: 0.95rem; line-height: 1.5;">OpenAI API를 활용하여 접속한 Github Repository 및 Code를 자동으로 요약해주는 Chrome Extension 개발.</p>
    <div style="display: flex; flex-wrap: wrap; gap: 8px; margin-top: 15px;">
      <span style="background-color: #f5eef8; color: #8e44ad; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Vanilla JS</span>
      <span style="background-color: #f5eef8; color: #8e44ad; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">Javascript</span>
      <span style="background-color: #f5eef8; color: #8e44ad; padding: 5px 10px; border-radius: 5px; font-size: 0.8rem;">OpenAI API</span>
    </div>
  </div>
</div>

</div>


<!-- 프로젝트 카드에 호버 효과를 추가하는 스타일 -->
<style>
.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.15);
}
.project-card img:hover {
  transform: scale(1.05);
}
.project-card a:hover {
  opacity: 0.9;
}
</style>

<!-- 모달 스타일 -->
<style>
/* 팝오버 스타일 */
.popover {
  display: none;
  position: absolute;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.2);
  padding: 15px;
  max-width: 450px;
  z-index: 1000;
  transition: opacity 0.3s ease, transform 0.3s ease;
  opacity: 0;
  transform: translateY(10px);
}

.popover.show {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.popover-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 15px;
}

.popover-header h3 {
  margin: 0;
  font-size: 1.2rem;
  color: #2c3e50;
}

.close-popover {
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
  color: #999;
}

.popover-content {
  max-height: 350px;
  overflow-y: auto;
}

.popover-footer {
  margin-top: 15px;
  text-align: right;
  border-top: 1px solid #eee;
  padding-top: 10px;
}

.popover-btn {
  padding: 6px 12px;
  background-color: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  text-decoration: none;
  display: inline-block;
  font-size: 0.8rem;
}

.popover-btn:hover {
  background-color: #2980b9;
}

/* 모달 스타일은 유지(다른 모달이 있을 수 있음) */
.modal {
  display: none;
  position: fixed;
  z-index: 1000;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0,0,0,0.7);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.modal.show {
  display: block;
  opacity: 1;
}

.modal-content {
  background-color: #fff;
  margin: 10% auto;
  padding: 20px;
  width: 80%;
  max-width: 800px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
  transform: translateY(-50px);
  transition: transform 0.3s ease;
}

.modal.show .modal-content {
  transform: translateY(0);
}

.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid #eee;
  padding-bottom: 10px;
  margin-bottom: 20px;
}

.close-modal {
  font-size: 28px;
  font-weight: bold;
  cursor: pointer;
}

.modal-image-gallery {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}

.modal-image-gallery img {
  max-width: 100%;
  height: auto;
  border-radius: 5px;
}

.modal-description {
  margin-bottom: 20px;
}

.modal-footer {
  display: flex;
  gap: 10px;
  justify-content: flex-end;
  border-top: 1px solid #eee;
  padding-top: 15px;
  flex-wrap: wrap;
}

.modal-btn {
  padding: 8px 15px;
  background-color: #333;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  display: inline-block;
}

.modal-btn:hover {
  background-color: #555;
}
</style>

<!-- DevZip 프로젝트 모달 -->
<div id="devzipModal" class="modal">
  <div class="modal-content">
    <div class="modal-header">
      <h3>DEV ZIP - 실험적 아이디어와 실서비스 프로젝트 쇼케이스</h3>
      <span class="close-modal">&times;</span>
    </div>
    <div class="modal-image-gallery">
      <img src="../../../../assets/images/devzip/logdashboard.png" alt="로그 대시보드">
      <img src="../../../../assets/images/devzip/eventlog.png" alt="이벤트 로그 분석">
      <img src="../../../../assets/images/devzip/humantrace.png" alt="히트맵 분석">
    </div>
    <div class="modal-description">
      <p>다양한 실험적 아이디어와 실서비스 프로젝트를 한곳에 모아놓은 플랫폼입니다. 방명록, 농담 API, 물리 퀴즈 등 재미있는 실험부터 트레이스보드, 트렌드챗 같은 실용적인 서비스까지 다양한 프로젝트를 선보입니다.</p>
      <ul>
        <li>사용 기술: Next.js, React, Node.js, Express, MongoDB, AWS</li>
        <li>개발 기간: 2024 ~ 현재</li>
        <li>주요 프로젝트:
          <ul>
            <li>트레이스보드: 웹사이트 분석을 위한 경량화된 솔루션</li>
            <li>트렌드챗: 실시간 기술 트렌드 정보 제공</li>
            <li>방명록, 농담 API, 물리 퀴즈 등 다양한 실험 프로젝트</li>
            <li>대시보드: 시스템 모니터링 및 로그 분석</li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="modal-footer" style="display: flex; gap: 10px; justify-content: flex-end; flex-wrap: wrap;">
      <button onclick="window.location.href='https://devzip.cloud';" style="text-decoration: none; border: none; display: inline-block; background-color: #333; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">사이트 방문</button>
      <span style="color: #e74c3c; font-size: 0.9rem; margin-left: 8px;">(※ 현재 서버 비용 문제로 서비스가 일시 중단되었습니다)</span>
      <button onclick="window.location.href='https://github.com/Hoooon22/';" style="text-decoration: none; border: none; display: inline-block; background-color: #333; color: white; padding: 8px 15px; border-radius: 5px; font-size: 0.9rem; transition: background-color 0.3s ease; cursor: pointer;">GitHub</button>
    </div>
  </div>
</div>

<!-- DevZip 프로젝트 요약 팝오버 -->
<div id="devzipSummaryPopover" class="popover">
  <div class="popover-header">
    <h3>DEV ZIP - 개발 과정 요약</h3>
    <span class="close-popover">&times;</span>
  </div>
  <div class="popover-content">
    <h4>개발 과정 타임라인</h4>
    <ul style="list-style-type: none; padding-left: 0;">
      <li style="margin-bottom: 15px; position: relative; padding-left: 25px;">
        <span style="position: absolute; left: 0; color: #3498db;">🔹</span>
        <strong>2024년 7월 초 - 프로젝트 시작</strong>
        <p>AWS 환경 구축 (EC2, RDS), 도메인 구매 (devzip.cloud), SpringBoot + React 개발환경 설정</p>
      </li>
      <li style="margin-bottom: 15px; position: relative; padding-left: 25px;">
        <span style="position: absolute; left: 0; color: #3498db;">🔹</span>
        <strong>2024년 7월 중순 - 기본 기능 개발</strong>
        <p>메인 페이지 레이아웃 디자인, 게스트북 기능 구현, 데이터베이스 연동</p>
      </li>
      <li style="margin-bottom: 15px; position: relative; padding-left: 25px;">
        <span style="position: absolute; left: 0; color: #3498db;">🔹</span>
        <strong>2025년 2월 - TrendChat 개발</strong>
        <p>Python 스크립트 자동화로 트렌드 데이터 수집, JSON 파일 저장 시스템 구현</p>
      </li>
      <li style="margin-bottom: 15px; position: relative; padding-left: 25px;">
        <span style="position: absolute; left: 0; color: #3498db;">🔹</span>
        <strong>2025년 4월 - 트레이스보드 개발</strong>
        <p>웹사이트 분석을 위한 경량화된 솔루션 개발, 방문자 지표, 사용자 행동 차트, 실시간 이벤트 로그 기능 구현</p>
      </li>
    </ul>

    <h4>주요 도전 과제와 해결책</h4>
    <ul>
      <li style="margin-bottom: 10px;"><strong>IP 주소 수집 이슈</strong> - AWS 로드 밸런서 설정 조정으로 X-Forwarded-For 헤더를 활용해 해결</li>
      <li style="margin-bottom: 10px;"><strong>데이터 수집 자동화</strong> - GitHub Actions와 pm2를 활용한 Python 스크립트 자동화로 해결</li>
      <li style="margin-bottom: 10px;"><strong>배포 프로세스 안정성</strong> - 단일 작업에서 4단계 파이프라인으로 개선하여 에러 추적 용이</li>
      <li style="margin-bottom: 10px;"><strong>사용자 행동 추적 개인정보 보호</strong> - IP 주소 마스킹 처리 등 개인정보 보호 방안 구현</li>
    </ul>

    <h4>기술 스택</h4>
    <div style="display: flex; flex-wrap: wrap; gap: 10px; margin-top: 10px;">
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">SpringBoot</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">React</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">Next.js</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">AWS EC2</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">AWS RDS</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">GitHub Actions</span>
      <span style="background-color: #e3f2fd; color: #0077b5; padding: 5px 10px; border-radius: 5px; font-size: 0.9rem;">Python</span>
    </div>
  </div>
  <div class="popover-footer">
    <a href="https://hoooon22.github.io/docs/projects/devzip/devzip/" class="popover-btn">모든 글 보기</a>
  </div>
</div>

<!-- 프로젝트 카드에 버튼 추가 -->
<script>
// 팝오버 관련 변수
let activePopover = null;

// 팝오버 열기 함수
function toggleCustomPopover(popoverId, button) {
  // 이미 열린 팝오버가 있으면 닫기
  if (activePopover) {
    closePopover(activePopover);
  }
  
  const popover = document.getElementById(popoverId);
  if (!popover) {
    console.error("Popover not found:", popoverId);
    return;
  }
  
  // 버튼 위치 기준으로 팝오버 위치 설정
  const buttonRect = button.getBoundingClientRect();
  const scrollTop = window.pageYOffset || document.documentElement.scrollTop;
  
  // 팝오버 위치 설정 (버튼 아래에 표시)
  popover.style.top = (buttonRect.bottom + scrollTop + 10) + 'px';
  popover.style.left = buttonRect.left + 'px';
  
  // 팝오버가 화면 오른쪽 경계를 벗어나지 않도록 조정
  setTimeout(() => {
    const popoverRect = popover.getBoundingClientRect();
    const windowWidth = window.innerWidth;
    
    if (popoverRect.right > windowWidth) {
      popover.style.left = (windowWidth - popoverRect.width - 20) + 'px';
    }
  }, 0);
  
  // 팝오버 표시
  popover.classList.add('show');
  activePopover = popover;
  
  // 클릭 이벤트 리스너 추가 (팝오버 외부 클릭 시 닫기)
  setTimeout(() => {
    document.addEventListener('click', documentClickHandler);
  }, 10);
  
  console.log("Popover opened:", popoverId);
}

// 팝오버 닫기 함수
function closePopover(popover) {
  if (!popover) return;
  
  popover.classList.remove('show');
  activePopover = null;
  
  // 클릭 이벤트 리스너 제거
  document.removeEventListener('click', documentClickHandler);
  
  console.log("Popover closed");
}

// 문서 클릭 이벤트 핸들러 (팝오버 외부 클릭 시 닫기)
function documentClickHandler(e) {
  if (activePopover) {
    const isClickInside = activePopover.contains(e.target) || 
                          e.target.classList.contains('popover-btn') || 
                          e.target.hasAttribute('data-popover') || 
                          (e.target.tagName === 'BUTTON' && e.target.getAttribute('onclick') && e.target.getAttribute('onclick').includes('toggleCustomPopover'));
    
    if (!isClickInside) {
      closePopover(activePopover);
    }
  }
}

// 모달 열기 함수 (기존 모달용)
function openModal(modalId) {
  console.log("Opening modal:", modalId);
  const modal = document.getElementById(modalId);
  if (!modal) {
    console.error("Modal not found:", modalId);
    return;
  }
  
  // 모달 표시
  modal.classList.add('show');
  
  // 배경 스크롤 방지
  document.body.style.overflow = 'hidden';
  
  console.log("Modal opened:", modalId);
}

// 모달 닫기 함수
function closeModal(modal) {
  console.log("Closing modal");
  modal.classList.remove('show');
  
  // 배경 스크롤 다시 활성화
  document.body.style.overflow = '';
}

// ESC 키 누를 때 모달과 팝오버 닫기
document.addEventListener('keydown', function(e) {
  if (e.key === 'Escape') {
    const openModal = document.querySelector('.modal.show');
    if (openModal) {
      closeModal(openModal);
    }
    
    if (activePopover) {
      closePopover(activePopover);
    }
  }
});

// 모달 배경 클릭 시 닫기
document.addEventListener('click', function(e) {
  const openModal = document.querySelector('.modal.show');
  if (openModal && e.target === openModal) {
    closeModal(openModal);
  }
});

// 스크롤 시 팝오버 닫기
window.addEventListener('scroll', function() {
  if (activePopover) {
    closePopover(activePopover);
  }
});

// 창 크기 변경 시 팝오버 닫기
window.addEventListener('resize', function() {
  if (activePopover) {
    closePopover(activePopover);
  }
});

// 페이지 로드 완료 후 모달 버튼에 이벤트 리스너 추가
document.addEventListener('DOMContentLoaded', function() {
  // 모달 버튼에 이벤트 리스너 추가
  const detailBtns = document.querySelectorAll('.detail-btn');
  detailBtns.forEach(function(btn) {
    const modalId = btn.getAttribute('data-modal');
    btn.addEventListener('click', function(e) {
      e.preventDefault();
      openModal(modalId);
    });
  });

  // 모달 닫기 버튼에 이벤트 리스너 추가
  const closeModalBtns = document.querySelectorAll('.close-modal');
  closeModalBtns.forEach(function(btn) {
    btn.addEventListener('click', function() {
      const modal = this.closest('.modal');
      closeModal(modal);
    });
  });

  // 팝오버 닫기 버튼에 이벤트 리스너 추가
  const closePopoverBtns = document.querySelectorAll('.close-popover');
  closePopoverBtns.forEach(function(btn) {
    btn.addEventListener('click', function(e) {
      e.stopPropagation();
      const popover = this.closest('.popover');
      closePopover(popover);
    });
  });
});

// 이미 문서가 로드되었다면 즉시 실행
if (document.readyState === 'complete' || document.readyState === 'interactive') {
  setTimeout(function() {
    // 모달 버튼에 이벤트 리스너 추가
    const detailBtns = document.querySelectorAll('.detail-btn');
    detailBtns.forEach(function(btn) {
      const modalId = btn.getAttribute('data-modal');
      btn.addEventListener('click', function(e) {
        e.preventDefault();
        openModal(modalId);
      });
    });

    // 모달 닫기 버튼에 이벤트 리스너 추가
    const closeModalBtns = document.querySelectorAll('.close-modal');
    closeModalBtns.forEach(function(btn) {
      btn.addEventListener('click', function() {
        const modal = this.closest('.modal');
        closeModal(modal);
      });
    });

    // 팝오버 닫기 버튼에 이벤트 리스너 추가
    const closePopoverBtns = document.querySelectorAll('.close-popover');
    closePopoverBtns.forEach(function(btn) {
      btn.addEventListener('click', function(e) {
        e.stopPropagation();
        const popover = this.closest('.popover');
        closePopover(popover);
      });
    });
  }, 0);
}
</script>

<!-- 인라인 스크립트로 직접 실행 -->
<script>
// 함수가 정의되었는지 확인
window.checkFunctionsInterval = setInterval(function() {
  if (typeof toggleCustomPopover === 'function' && typeof openModal === 'function') {
    clearInterval(window.checkFunctionsInterval);
    console.log("모든 함수가 로드되었습니다.");
    
    // 모달 버튼에 이벤트 리스너 추가
    document.querySelectorAll('.detail-btn').forEach(function(btn) {
      const modalId = btn.getAttribute('data-modal');
      btn.onclick = function(e) {
        e.preventDefault();
        openModal(modalId);
      };
    });
    
    // 모달 닫기 버튼에 이벤트 리스너 추가
    document.querySelectorAll('.close-modal').forEach(function(btn) {
      btn.onclick = function() {
        const modal = this.closest('.modal');
        closeModal(modal);
      };
    });
    
    // 팝오버 닫기 버튼에 이벤트 리스너 추가
    document.querySelectorAll('.close-popover').forEach(function(btn) {
      btn.onclick = function(e) {
        e.stopPropagation();
        const popover = this.closest('.popover');
        closePopover(popover);
      };
    });
  }
}, 100);
</script>

---

```java
if (code.isWorks()) {
    return Best_Moment; // :)
}
```