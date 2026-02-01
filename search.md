---
layout: page
title: Tìm Kiếm
permalink: /search/
---

# Tìm Kiếm Tài Liệu

Sử dụng công cụ tìm kiếm dưới đây để nhanh chóng tìm thấy thông tin bạn cần trong tài liệu OpenClaw tiếng Việt.

<form action="/search/" method="get">
  <label for="search-box">Tìm kiếm:</label>
  <input type="text" id="search-box" name="query" placeholder="Nhập từ khóa cần tìm...">
  <input type="submit" value="Tìm">
</form>

<div id="results">
  <!-- Kết quả tìm kiếm sẽ hiển thị ở đây -->
</div>

<script>
  // JavaScript đơn giản để tìm kiếm trong tài liệu
  // Lưu ý: Đây là phiên bản đơn giản, trên production nên dùng giải pháp tìm kiếm nâng cao hơn
  
  // Danh sách các trang để tìm kiếm
  const pages = [
    { title: "Bắt đầu với OpenClaw", url: "/docs/getting-started/", content: "hướng dẫn cài đặt và chạy OpenClaw từ con số 0" },
    { title: "Kết nối WhatsApp", url: "/docs/channels/whatsapp/", content: "hướng dẫn kết nối OpenClaw với WhatsApp" },
    { title: "Khái niệm cốt lõi", url: "/docs/concepts/", content: "giải thích các khái niệm chính của OpenClaw" },
    { title: "Công cụ & Kỹ năng", url: "/docs/tools/", content: "hướng dẫn sử dụng công cụ và kỹ năng trong OpenClaw" },
    { title: "Gateway & Hệ thống", url: "/docs/gateway/", content: "hiểu rõ cách gateway hoạt động" },
    { title: "Giới thiệu", url: "/about/", content: "giới thiệu về dự án tài liệu OpenClaw tiếng Việt" }
  ];

  // Hàm tìm kiếm
  function performSearch() {
    const query = document.getElementById('search-box').value.toLowerCase();
    const resultsDiv = document.getElementById('results');
    
    if (!query) {
      resultsDiv.innerHTML = '<p>Vui lòng nhập từ khóa để tìm kiếm.</p>';
      return;
    }
    
    const results = pages.filter(page => 
      page.title.toLowerCase().includes(query) || 
      page.content.toLowerCase().includes(query)
    );
    
    if (results.length === 0) {
      resultsDiv.innerHTML = '<p>Không tìm thấy kết quả nào phù hợp với từ khóa "' + query + '".</p>';
      return;
    }
    
    let resultsHtml = '<h3>Kết quả tìm kiếm cho: "' + query + '"</h3><ul>';
    results.forEach(result => {
      resultsHtml += '<li><a href="' + result.url + '">' + result.title + '</a><br>' +
                     '<small>' + result.content + '</small></li>';
    });
    resultsHtml += '</ul>';
    
    resultsDiv.innerHTML = resultsHtml;
  }

  // Gắn sự kiện submit form
  document.querySelector('form').addEventListener('submit', function(e) {
    e.preventDefault();
    performSearch();
  });

  // Nếu có tham số tìm kiếm trong URL, thực hiện tìm kiếm
  const urlParams = new URLSearchParams(window.location.search);
  const searchQuery = urlParams.get('query');
  if (searchQuery) {
    document.getElementById('search-box').value = searchQuery;
    performSearch();
  }
</script>