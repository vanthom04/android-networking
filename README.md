# Android Networking

## [Thư viện Volley](https://google.github.io/volley/)

Install:
``implementation("com.android.volley:volley:1.2.1")``

<div id="markdown-content">
  This is some Markdown content that you want to copy.
</div>

<button onclick="copyToClipboard()">Copy</button>

<script>
function copyToClipboard() {
  const markdownContent = document.getElementById("markdown-content").textContent;
  const textArea = document.createElement("textarea");
  textArea.value = markdownContent;
  document.body.appendChild(textArea);
  textArea.select();
  document.execCommand("copy");
  document.body.removeChild(textArea);
  alert("Text copied to clipboard!");
}
</script>
