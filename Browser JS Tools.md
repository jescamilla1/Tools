# Debug Bookmarklets


## Highlight Form Fields

Outlines every `input`, `select`, and `textarea` on the page in red, and labels each with its `name` attribute.

**Use case:** quickly identify all form fields and their `name` attrs on a page — useful for mapping form fields to CFC method params or `form.` scope variables.

```javascript
javascript:(function(){document.querySelectorAll('input,select,textarea').forEach(function(el){el.style.outline='2px solid red';var t=document.createElement('div');t.textContent=el.name||'(no name)';t.style.cssText='position:absolute;background:yellow;font-size:10px;z-index:9999';el.parentNode.insertBefore(t,el)})})()
```

## Audit CSS (Layout Marker)

Click to activate: hover any `div` to outline it and show a live panel (bottom-left) with tag/id/class, size, `display`, `position`, `margin`, `padding`, plus flex/grid-specific properties when relevant. Click again to deactivate.

**Use case:** inspect layout structure and box-model values without opening devtools — handy for fixing UI/layout issues on dense CF admin pages.

```javascript
javascript:(function(){var old=document.getElementById('_layoutMarker');if(old){old.remove();document.querySelectorAll('.__lm_hi').forEach(function(el){el.style.outline='';});return}var tip=document.createElement('div');tip.id='_layoutMarker';tip.style.cssText='position:fixed;bottom:10px;left:10px;background:#111;color:#0f0;font:11px monospace;padding:8px;z-index:99999;max-width:400px;white-space:pre;pointer-events:none;border:1px solid #0f0';document.body.appendChild(tip);document.querySelectorAll('div').forEach(function(el){el.addEventListener('mouseenter',function(e){e.stopPropagation();el.classList.add('__lm_hi');el.style.outline='1px solid red';var cs=getComputedStyle(el);var r=el.getBoundingClientRect();tip.textContent='div'+(el.id?'#'+el.id:'')+(el.className?'.'+String(el.className).replace(/ /g,'.'):'')+'\nsize: '+Math.round(r.width)+'x'+Math.round(r.height)+'\ndisplay: '+cs.display+'\nposition: '+cs.position+'\nmargin: '+cs.margin+'\npadding: '+cs.padding+(cs.display.indexOf('flex')>-1?'\nflex-dir: '+cs.flexDirection+'\njustify: '+cs.justifyContent+'\nalign: '+cs.alignItems:'')+(cs.display.indexOf('grid')>-1?'\ngrid-template: '+cs.gridTemplateColumns:'')});el.addEventListener('mouseleave',function(){el.classList.remove('__lm_hi');el.style.outline=''})})})()
```

## Installation

1. Open bookmarks bar in your browser (Ctrl/Cmd + Shift + B)
2. Right-click → Add page / New bookmark
3. Name it (e.g. "Highlight Form Fields")
4. Paste the full `javascript:...` snippet as the URL
5. Click the bookmark on any page to run it
