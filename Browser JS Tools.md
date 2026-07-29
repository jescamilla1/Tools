Highlight Form Fields 

'''
javascript:(function(){document.querySelectorAll('input,select,textarea').forEach(function(el){el.style.outline='2px solid red';var t=document.createElement('div');t.textContent=el.name||'(no name)';t.style.cssText='position:absolute;background:yellow;font-size:10px;z-index:9999';el.parentNode.insertBefore(t,el)})})()
'''

Audit CSS

'''
javascript:(function(){var old=document.getElementById('_layoutMarker');if(old){old.remove();document.querySelectorAll('.__lm_hi').forEach(function(el){el.style.outline='';});return}var tip=document.createElement('div');tip.id='_layoutMarker';tip.style.cssText='position:fixed;bottom:10px;left:10px;background:#111;color:#0f0;font:11px%20monospace;padding:8px;z-index:99999;max-width:400px;white-space:pre;pointer-events:none;border:1px%20solid%20#0f0';document.body.appendChild(tip);document.querySelectorAll('div').forEach(function(el){el.addEventListener('mouseenter',function(e){e.stopPropagation();el.classList.add('__lm_hi');el.style.outline='1px%20solid%20red';var%20cs=getComputedStyle(el);var%20r=el.getBoundingClientRect();tip.textContent='div'+(el.id?'#'+el.id:'')+(el.className?'.'+String(el.className).replace(/%20/g,'.'):'')+'\nsize:%20'+Math.round(r.width)+'x'+Math.round(r.height)+'\ndisplay:%20'+cs.display+'\nposition:%20'+cs.position+'\nmargin:%20'+cs.margin+'\npadding:%20'+cs.padding+(cs.display.indexOf('flex')%3E-1?'\nflex-dir:%20'+cs.flexDirection+'\njustify:%20'+cs.justifyContent+'\nalign:%20'+cs.alignItems:'')+(cs.display.indexOf('grid')%3E-1?'\ngrid-template:%20'+cs.gridTemplateColumns:'')});el.addEventListener('mouseleave',function(){el.classList.remove('__lm_hi');el.style.outline=''})})})()
'''
