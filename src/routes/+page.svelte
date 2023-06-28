<script lang="ts">
  import { Accordion, AccordionItem } from '$lib/components/accordion'
  
  const items = [
  { title: 'Item 1', content: 'Content 1' },
  { title: 'Item 2', content: 'Content 2' },
  { title: 'Item 3', content: 'Content 3' },
  { title: 'Item 4', content: 'Content 4' }
  ]
</script>

<Accordion>
  <AccordionItem>
    <div slot="title">Item 1</div>
    <div slot="content">Content 1</div>
  </AccordionItem>
</Accordion>

<Accordion>
  <AccordionItem>
    <div slot="title">Item 2</div>
    <div slot="content">Content 2</div>
  </AccordionItem>
</Accordion>