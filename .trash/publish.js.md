let footer = document.getElementsByClassName("site-footer");
for (let child of footer.children) {
	if (child.nodeName == "P" && child.getAttribute(href) == "https://publish.obsidian.md/") {
		child.remove();
		break;
	}
}