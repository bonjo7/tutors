<script lang="ts">
	import ExperienceCard from './ExperienceCard.svelte';

	const title = 'Developer Experience';
	const icon = 'ant-design:code-outlined';
	const link = 'https://reader.tutors.dev/lab/tutors-docs/topic-03-DX/unit-0/book-plans/03';
	const content = `
  The <strong><em>Developer Experience</em></strong> prioritises the specification and implementation of <strong>robust</strong>, <strong>well documented</strong>,
  <strong>loosely coupled components & services</strong>, integrated into a
  <strong>coherent toolkit</strong>
  open to contributions from <strong>diverse skill sets</strong>.
  `;
</script>

<ExperienceCard {title} {icon} {link} {content} />
