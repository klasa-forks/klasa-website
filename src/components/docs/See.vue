<template>
	<div>
		<strong>See also:</strong>

		<ul v-if="see.length > 1">
			<li v-for="(s, i) in parsed" :key="i">
				<router-link v-if="typeof s.link === 'object'" :to="s.link">
					{{ s.text }}
				</router-link>
				<a v-else-if="typeof s.link === 'string'" :href="s.link">
					{{ s.text }}
				</a>
				<span v-else>
					{{ s.text }}
				</span>
			</li>
		</ul>

		<span v-else>
			<router-link v-if="typeof parsed[0].link === 'object'" :to="parsed[0].link">
				{{ parsed[0].text }}
			</router-link>
			<a v-else-if="typeof parsed[0].link === 'string'" :href="parsed[0].link">
				{{ parsed[0].text }}
			</a>
			<span v-else>
				{{ parsed[0].text }}
			</span>
		</span>
	</div>
</template>

<script>
import { parseLink } from '../../util';

export default {
	name: 'DocsSee',
	props: ['see', 'docs'],

	computed: {
		parsed() {
			const parsed = new Array(this.see.length);
			for (let i = 0; i < this.see.length; i++) parsed[i] = parseLink(this.see[i], undefined, this.docs);
			return parsed;
		}
	}
};
</script>

