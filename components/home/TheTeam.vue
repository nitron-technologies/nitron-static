<template>
	<section class="container">
		<h2 id="team">The Team</h2>
		<div class="members">
			<HomeTeamMember
				v-for="member in members"
				:key="member.name"
				:name="member.name"
				:position="member.position"
				:headshot="member.headshot"
				:description="member.description"
				:right="members.indexOf(member) % 2 === 1"
			/>
		</div>
	</section>
</template>

<style lang="scss" scoped>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
	}
	#team {
		background-color: var(--color-secondary);
		color: white;
		font-size: 5vw;
		width: calc(100% - 2rem);
		padding: 1rem;
		align-self: flex-start;
	}
	.members {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(10rem, 1fr));
		padding: 2rem;
		max-width: 65rem;
	}
	@media screen and (max-width: 60rem) {
		#team {
			font-size: 6.5vw;
		}
	}
	@media screen and (max-width: 40rem) {
		#team {
			font-size: 8vw;
		}
	}
</style>

<script lang="ts">
	import { defineComponent } from "vue";
	interface TeamMember {
		name: string;
		position: string;
		headshot: string;
		description: string;
	}

	export default defineComponent({
		async created() {
			const response = await this.$content("team").fetch();
			this.members = (Array.isArray(response) ? response[0].members : response.members) as unknown as TeamMember[];
		},

		data(): { members: TeamMember[] } {return {members: []}},
	});
</script>