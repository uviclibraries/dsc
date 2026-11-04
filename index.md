---
layout: default
title: DSC Workshop Lesson Plans 
nav_order: 1
---

<img src="images/dsc-logo.png" style="float:right;width:180px;" alt="DSC Logo">

# DSC Workshop Lesson Plans

Check out our full list of [**upcoming scheduled workshops**](https://libcal.uvic.ca/calendar/dsc?cid=7692&t=g&d=0000-00-00&cal=7692&inc=0){:target="_blank"}! If you have any questions about our workshops or are an instructor wanting to have us run one of our workshops in connection with your course, feel free to [send us an email](mailto:rmccue@uvic.ca?Subject=Workshop%20Request){:target="_blank"}. If you would like to be kept up to date with DSC announcements, including new workshops, you can sign up for our [low-volume email list here](https://e1.envoke.com/ext/pages/7ca0996db17fcc4be7f60392f6790490){:target="_blank"}.

Below are self-drected workshops that the DSC has made available for anyone in the world to use free of charge!  

---

{::nomarkdown}
<div id="dsc-workshop-filter-widget" class="dsc-filter-container">
  <label for="dsc-workshop-search-input" class="dsc-filter-label">Filter workshops on this page:</label>
  <div class="dsc-search-input-group">
    <input type="search" id="dsc-workshop-search-input" class="dsc-search-input" placeholder="e.g., spreadsheet, Python, Canva..." autocomplete="off" spellcheck="false" />
    <button type="button" id="dsc-clear-button" class="dsc-clear-btn" aria-label="Clear filter search">Clear</button>
  </div>
  <div id="dsc-search-status" class="dsc-search-status" aria-live="polite"></div>
</div>

<style>
/* Base widget styles */
.dsc-filter-container {
  box-sizing: border-box;
  margin: 1rem 0;
  padding: 1rem 1.1rem;
  background-color: #f8f9fa;
  border: 1px solid #e1e4e8;
  border-radius: 6px;
  font-family: inherit;
}
.dsc-filter-label {
  display: block;
  font-weight: 600;
  margin-bottom: 0.45rem;
  font-size: 0.92rem;
  color: #24292e;
}
.dsc-search-input-group {
  display: flex;
  gap: 0.4rem;
  align-items: center;
}
.dsc-search-input {
  flex: 1;
  padding: 0.5rem 0.65rem;
  font-size: 0.95rem;
  border: 1px solid #c8ccd0;
  border-radius: 4px;
  outline: none;
  background: #ffffff;
  box-sizing: border-box;
}
.dsc-search-input:focus {
  border-color: #0366d6;
  box-shadow: 0 0 0 3px rgba(3, 102, 214, 0.2);
}
.dsc-clear-btn {
  padding: 0.5rem 0.8rem;
  font-size: 0.88rem;
  border: 1px solid #d1d5da;
  border-radius: 4px;
  background: #ffffff;
  cursor: pointer;
  color: #444d56;
  white-space: nowrap;
}
.dsc-clear-btn:hover {
  background-color: #f3f4f6;
  color: #24292e;
}
.dsc-search-status {
  margin-top: 0.5rem;
  font-size: 0.85rem;
  color: #586069;
  min-height: 1.1rem;
}
.dsc-reset-link {
  color: #0366d6;
  text-decoration: underline;
  cursor: pointer;
}
.dsc-item-hidden {
  display: none !important;
}

/* Side-by-side floating layout for tablet & desktop */
@media (min-width: 768px) {
  .dsc-filter-container {
    float: right;
    width: 48%;
    margin: 0 0 1.5rem 2%;
  }
  /* Target the Jump-link blockquote sitting immediately next to the widget */
  .dsc-filter-container + blockquote,
  blockquote:has(+ .dsc-filter-container) {
    float: left;
    width: 48%;
    margin: 0 2% 1.5rem 0 !important;
    box-sizing: border-box;
  }
  /* Clearfix on the following HR or H2 to keep workshops neatly below both blocks */
  .dsc-filter-container ~ hr,
  .dsc-filter-container ~ h2 {
    clear: both;
  }
}
</style>

<script>
(function() {
  var SYNONYMS = {
    'xls': 'spreadsheet data sheets excel',
    'rstud': 'statistics stats r rstudio data',
    'rvis': 'charts graphics visualization r rstudio ggplot',
    'rintr': 'advanced stats programming r rstudio',
    'nvivo': 'qualitative coding text analysis',
    'nvadv': 'qualitative coding advanced',
    'qualcoder': 'qualitative coding python open source',
    'tag': 'qualitative coding text analysis open source',
    'qgis': 'gis maps spatial geographic spatial-data raster vector',
    'html': 'web coding web-design development frontend website',
    'photopea': 'photoshop image-editing raster graphics',
    'gimp': 'photoshop image-editing raster graphics open source',
    'fusion360': 'cad 3d-printing fabrication modeling autodesk',
    'blender': '3d modeling animation graphics',
    'ard': 'microcontroller electronics physical computing hardware',
    'iot': 'hardware internet smart electronics sensor arduino',
    'raspi': 'linux computer single-board hardware raspberry pi',
    'gen-ai': 'artificial intelligence llm chatgpt prompt',
    'vibe-code': 'programming coding apps software ai development',
    'genai': 'artificial intelligence llm prompt agents'
  };

  function initFilter() {
    var widget = document.getElementById('dsc-workshop-filter-widget');
    var input = document.getElementById('dsc-workshop-search-input');
    var clearBtn = document.getElementById('dsc-clear-button');
    var status = document.getElementById('dsc-search-status');
    if (!widget || !input || !clearBtn || !status) return;

    var container = widget.parentElement || document.body;
    var blockquote = container.querySelector('blockquote');
    var hrAfterBlockquote = null;
    if (blockquote) {
      var next = blockquote.nextElementSibling;
      while (next && next.tagName.toLowerCase() !== 'h2') {
        if (next.tagName.toLowerCase() === 'hr') {
          hrAfterBlockquote = next;
          break;
        }
        next = next.nextElementSibling;
      }
    }

    var h2Elements = Array.from(container.querySelectorAll('h2')).filter(function(h2) {
      if (h2.closest('blockquote')) return false;
      if (h2.textContent.toLowerCase().indexOf('jump directly') !== -1) return false;
      return true;
    });

    var categoryPairs = [];
    h2Elements.forEach(function(h2) {
      var sibling = h2.nextElementSibling;
      var uls = [];
      while (sibling && sibling.tagName.toLowerCase() !== 'h2') {
        if (sibling.tagName.toLowerCase() === 'ul') {
          uls.push(sibling);
        }
        sibling = sibling.nextElementSibling;
      }
      var items = [];
      uls.forEach(function(ul) {
        Array.from(ul.querySelectorAll('li')).forEach(function(li) {
          var text = li.textContent.toLowerCase();
          var links = Array.from(li.querySelectorAll('a')).map(function(a) { return a.href.toLowerCase(); }).join(' ');
          var dataKeywords = (li.getAttribute('data-keywords') || '').toLowerCase();
          var synonymKeywords = '';
          for (var key in SYNONYMS) {
            if (links.indexOf(key) !== -1) {
              synonymKeywords += ' ' + SYNONYMS[key];
            }
          }
          var searchIndex = text + ' ' + links + ' ' + dataKeywords + ' ' + synonymKeywords + ' ' + h2.textContent.toLowerCase();
          items.push({ element: li, index: searchIndex });
        });
      });
      if (items.length > 0) {
        categoryPairs.push({ h2: h2, uls: uls, items: items });
      }
    });

    var totalWorkshops = categoryPairs.reduce(function(acc, cat) { return acc + cat.items.length; }, 0);

    function escapeHtml(str) {
      return str.replace(/[&<>"']/g, function(m) {
        return { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[m];
      });
    }

    function runFilter() {
      var query = input.value.trim().toLowerCase();
      var tokens = query.split(/\s+/).filter(Boolean);

      // Hide blockquote and reset widget width when actively filtering
      if (tokens.length > 0) {
        if (blockquote) blockquote.classList.add('dsc-item-hidden');
        if (hrAfterBlockquote) hrAfterBlockquote.classList.add('dsc-item-hidden');
        widget.style.float = 'none';
        widget.style.width = '100%';
        widget.style.margin = '1rem 0';
      } else {
        if (blockquote) blockquote.classList.remove('dsc-item-hidden');
        if (hrAfterBlockquote) hrAfterBlockquote.classList.remove('dsc-item-hidden');
        widget.style.float = '';
        widget.style.width = '';
        widget.style.margin = '';
      }

      var totalMatches = 0;
      categoryPairs.forEach(function(category) {
        var categoryMatchCount = 0;
        category.items.forEach(function(item) {
          var matches = tokens.every(function(t) { return item.index.indexOf(t) !== -1; });
          if (matches) {
            item.element.classList.remove('dsc-item-hidden');
            categoryMatchCount++;
            totalMatches++;
          } else {
            item.element.classList.add('dsc-item-hidden');
          }
        });
        if (categoryMatchCount === 0 && tokens.length > 0) {
          category.h2.classList.add('dsc-item-hidden');
          category.uls.forEach(function(ul) { ul.classList.add('dsc-item-hidden'); });
        } else {
          category.h2.classList.remove('dsc-item-hidden');
          category.uls.forEach(function(ul) { ul.classList.remove('dsc-item-hidden'); });
        }
      });

      if (tokens.length === 0) {
        status.textContent = 'Showing all ' + totalWorkshops + ' workshops.';
      } else if (totalMatches === 0) {
        status.innerHTML = 'No workshops matched "<strong>' + escapeHtml(query) + '</strong>". <span class="dsc-reset-link" role="button" tabindex="0">Reset search</span>';
        var resetLink = status.querySelector('.dsc-reset-link');
        if (resetLink) {
          resetLink.addEventListener('click', resetFilter);
          resetLink.addEventListener('keydown', function(e) {
            if (e.key === 'Enter' || e.key === ' ') resetFilter();
          });
        }
      } else {
        var noun = totalMatches === 1 ? 'workshop' : 'workshops';
        status.textContent = 'Showing ' + totalMatches + ' matching ' + noun + '.';
      }

      try {
        var url = new URL(window.location.href);
        if (tokens.length > 0) {
          url.searchParams.set('q', query);
        } else {
          url.searchParams.delete('q');
        }
        window.history.replaceState({}, '', url.toString());
      } catch (err) {}
    }

    function resetFilter() {
      input.value = '';
      runFilter();
      input.focus();
    }

    input.addEventListener('input', runFilter);
    input.addEventListener('search', runFilter);
    clearBtn.addEventListener('click', resetFilter);

    try {
      var initialQuery = new URLSearchParams(window.location.search).get('q');
      if (initialQuery) {
        input.value = initialQuery;
      }
    } catch (e) {}

    runFilter();
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', initFilter);
  } else {
    initFilter();
  }
})();
</script>
{:/nomarkdown}

> ## Jump to a Workshop Category:
> - [Data Analysis, Visualization, Mapping & GIS](#data)
> - [Design & Media Production](#design)
> - [AI Workshop Pathway](#ai)
> - [Fabrication & Electronics](#fabrication)
> - [Research & Data Literacy Skills](#research)
> - [Archived Workshops](#archived)

---

## <a id="data"></a>Data Analysis, Visualization, Mapping & GIS
- [Data Analysis with Excel](https://lib.uvic.ca/xls){:target="_blank"}
- [RStudio Summary Statistics Introduction](https://lib.uvic.ca/rstud){:target="_blank"} 
- [RStudio Data Manipulation & Visualization Introduction](https://lib.uvic.ca/rvis){:target="_blank"} 
- [RStudio Data Analysis Intermediate](https://lib.uvic.ca/rintr){:target="_blank"}
- [Data Visualization & Narrative Maps](https://lib.uvic.ca/dvis){:target="_blank"} - Introduction
- [Intro to QGIS Map Print Layout](https://uviclibraries.github.io/qgis-printlayout){:target="_blank"} 
- [Intro to QGIS with Raster Data](https://uviclibraries.github.io/qgis-raster){:target="_blank"}
- [Intro to QGIS with Vector Data](https://uviclibraries.github.io/qgis-vector){:target="_blank"}
- [Edit Vector Data with QGIS](https://uviclibraries.github.io/qgis-editvector){:target="_blank"}
- [Infographics with Canva](https://lib.uvic.ca/ig){:target="_blank"}
- [Qualitative Data Analysis & Coding with NVIVO](https://lib.uvic.ca/nvivo){:target="_blank"}
- [Qualitative Data Analysis & Coding with NVIVO](https://lib.uvic.ca/nvadv){:target="_blank"} - Advanced
- [Qualitative Data Analysis & Coding with QualCoder](https://github.com/uviclibraries/qualcoder){:target="_blank"}
- [Qualitative Coding with Taguette](https://lib.uvic.ca/tag){:target="_blank"}
- [Tidy Data](https://lib.uvic.ca/tidy){:target="_blank"}

## <a id="design"></a>Design & Media Production
- [Academic Posters with Canva](https://lib.uvic.ca/apc){:target="_blank"}
- [Build a basic AI-free Website From Scratch: An Introduction to HTML and CSS](https://lib.uvic.ca/html){:target="_blank"}
- [Creating 360 Tours & Narrative Maps](https://lib.uvic.ca/vr360){:target="_blank"}
- [Design & Layout with Canva](https://lib.uvic.ca/dl){:target="_blank"} - Introduction
- [Death by PowerPoint](https://lib.uvic.ca/ppt-death){:target="_blank"} (Creating Pursuasive & Engaging Presentations)
- [Image Editing with Photopea](https://uviclibraries.github.io/image-editing-photopea/){:target="_blank"} (a free Adobe Photoshop alternative)
- [Interactive, Nonlinear Stories with Twine](https://lib.uvic.ca/tw){:target="_blank"}
- [Personal Websites with WordPress](https://lib.uvic.ca/wp){:target="_blank"}
- [Photography with your Smartphone](https://lib.uvic.ca/spp){:target="_blank"}
- [Podcasting with Audacity](https://lib.uvic.ca/pod){:target="_blank"}
- [Sketchnoting: Doodle Your Way to Better Grades](https://lib.uvic.ca/skn){:target="_blank"}
- [Video Editing with iMovie or Windows ClipChamp](https://lib.uvic.ca/vid){:target="_blank"} (Win, Mac)
- [Zine Making](https://lib.uvic.ca/zines){:target="_blank"}

## <a id="ai"></a>AI Workshops ([Link to AI Pathway](https://lib.uvic.ca/genai-pathway){:target="_blank"})
- [GenAI: Introduction & Prompt Design](https://lib.uvic.ca/gen-ai){:target="_blank"} (_Introduction_)
- [AI: Tools for Literature Reviews](https://lib.uvic.ca/ai-lit-search){:target="_blank"} (_Introduction_)
- [Is Your Smart Phone Listening to You? How to stop Big Tech from Tracking You Online](https://lib.uvic.ca/priv-sec){:target="_blank"} (_Introduction_)
- [Transcription with Free AI Tools](https://lib.uvic.ca/transcription){:target="_blank"} (_Intermediate_)
- [GenAI: Gemini Notebook a Personal Tool for Research & Productivity](https://lib.uvic.ca/genai-notebooklm){:target="_blank"} (_Intermediate_)
- [From Ideas to Apps: Create Apps & Learning Games with Generative AI](https://lib.uvic.ca/vibe-code-intro){:target="_blank"} (_Intermediate_)
- [GenAI: Research Tools](https://lib.uvic.ca/genai-research-adv){:target="_blank"} (_Advanced_)
- Create Local Apps for Research Using GenAI Vibe Coding Techniques (_Advanced_) - COMING FALL 2026 or SPRING 2027

## <a id="fabrication"></a>Fabrication & Electronics
- [3D Design & Print](https://lib.uvic.ca/3d){:target="_blank"} - Introduction
- [Design for Laser Cutting](https://lib.uvic.ca/lasdes){:target="_blank"}
- [Electronics with Arduino](https://lib.uvic.ca/ard){:target="_blank"}
- [Internet of Things with Arduino](https://lib.uvic.ca/iot){:target="_blank"}
- [Digital Design for Laser Cutting Woodblock Prints](https://lib.uvic.ca/woodblock){:target="_blank"}
- [Lasting Impressions: East Asian Seal Art Across Time and Media 2](https://lib.uvic.ca/seals){:target="_blank"}
- [Modelling in Blender](https://lib.uvic.ca/blender){:target="_blank"}
- [Resurrect Your Laptop with Linux](https://lib.uvic.ca/linux){:target="_blank"}

## <a id="research"></a>Research & Data Literacy Skills
- [Creating & Teaching Active Learning Workshops](https://lib.uvic.ca/alw){:target="_blank"}
- [Data Management Planning](https://lib.uvic.ca/dmp){:target="_blank"}

## <a id="archived"></a>Archived Workshops
- [3D Design with Autodesk Fusion](https://lib.uvic.ca/fusion360){:target="_blank"} - Intermediate
- [3D Scanning with Your Phone & KIRI Engine](https://lib.uvic.ca/kiri){:target="_blank"}
- [Audio Recording for Language Revitalization Games](https://lib.uvic.ca/audio-rev){:target="_blank"}
- [DataFrames in Pandas](https://uviclibraries.github.io/data-frames/){:target="_blank"} (Python)
- [Data Visualization with Tableau](https://lib.uvic.ca/tab){:target="_blank"} - Intermediate
- [Data Wrangling or cleaning with OpenRefine](https://lib.uvic.ca/or){:target="_blank"}
- [Electronics with Raspberry Pi](https://lib.uvic.ca/raspi){:target="_blank"} (Needs updating)
- [Interactive & Multimedia Website Content with H5P](https://lib.uvic.ca/h5p){:target="_blank"}
- [Image Editing with Adobe Photoshop](https://uviclibraries.github.io/photoshop/){:target="_blank"}
- [Image Editing with GIMP](https://lib.uvic.ca/gimp){:target="_blank"} (an open source Adobe Photoshop alternative)
- Knowledge Mobilization Skills (Can be requested as in-class workshop. No lesson plan link currently available)
- [Laser Cutting Ocean Floor Contour Maps](https://lib.uvic.ca/laser-maps){:target="_blank"}
- [Scientific Documents with Latex](https://lib.uvic.ca/lt){:target="_blank"}
- [Survey Creation with SurveyMonkey](https://lib.uvic.ca/survey){:target="_blank"}
- [Version Control with Github](https://lib.uvic.ca/github){:target="_blank"}
- [Website User Interface Design with Figma](https://lib.uvic.ca/figma){:target="_blank"}
