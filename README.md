\# Lovelace-layout-card-NO-MARGIN-in-a-no-nested-grid-layout  
The attempts to create a responsive dashboard with the layout-card

<img width="1280" height="960" alt="Naamloos document" src="https://github.com/user-attachments/assets/d756aa91-7ca4-4f09-91cb-93c4323a1a8e" />

Diving into the documentation https://github.com/thomasloven/lovelace-card-mod/tree/master  
learned me that it's sometimes complicated. Unfortunately I don’t want margins or paddings. I tested a non nested layout-card in different approaches that I found on the internet. Maybe there are more, please let me know.   
What needed to work was no margin and still be able to scale the sub card in portrait mode for example  
So instead of using the real dimensions of a card I would like to use 100%.  
To experiment I made a new dashboard with different views all based on the panel.  
I made 6 Markdown-card and 6 picture cards.

I found 3 ways to inflict change on the margin: 








**1) Layout margin 0px or \-4px**

This method seems to shrink the cards and removes the upper and left margin, unfortunately not the bottom margin   
```
  - path: layout-margin-settings
    title: layout-margin-settings
    type: panel
    cards:
      - type: custom:layout-card
        layout_type: custom:grid-layout
        layout:
          gap: 0px
          margin: '-4px 24px 35px -4px'
          padding: '-0px'
          grid-template-columns: repeat(6, 91.5px)
          grid-template-rows: auto
          grid-template-areas: |
```
<img width="1537" height="797" alt="image" src="https://github.com/user-attachments/assets/26e1888f-fc46-4529-960c-31eb671a0846" />

```
-- layout-margin: 14px 24px 35px 45px  
```

```
-- layout-margin: 14px -24px -35px 45px no change  
-- layout-margin: -14px 24px 35px -45px  change
```

**2) the mod-card**  
     
   This starts practically at the top..
```
views:  
  - path: mod-card test multiple cards
	title: mod-card test multiple cards
	type: panel
	cards:
	  - type: custom:mod-card
		style:
		  layout-card$:
			grid-layout$:
			  .: |
				#root > * {
				  margin: 0px !important;
				}
		card:  
   ```  
     
   The AI’s suggest it was a typo, but even in October  2025 it still works..

**3)  \--masonry-view-card-margin** 

   This is done inside every sub card  
```
        cards:
          - type: markdown
            content: |
              <div style="line-height: 1; margin: 0; padding: 0;">1</div>
            view_layout:
              grid-area: plaats1
            card_mod:
              style: |
                :host {
                  --masonry-view-card-margin: 0px;
                }
```

Option 2 and 3 seems to work, but when switching from portrait to landscape IMG 12 pops up way too big and it shouldn’t even be there.

What I found strange was that altough I only asked to see 9 cards in landscape the last card showed up way to big.
<img width="535" height="294" alt="image" src="https://github.com/user-attachments/assets/669175c1-c297-414c-ad43-3cfb0190f50a" />
<img width="315" height="422" alt="image" src="https://github.com/user-attachments/assets/7824e70b-492a-42a9-a83b-f9547affdad0" />

Even with the mod-card and changing the order of only shuffling the last card shows up?
Appearantly the cards are still rendered and can therefore show up. Tricks like "....." doesn't always seems to be relaible.



`      display: none` works but one can also just delete that card.

The complete dashboard code can be found in this repository
