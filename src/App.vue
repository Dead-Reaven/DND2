<template>
	<div class="app">
		<h1 :style="{ color: draggedMember ? 'red' : 'inherit' }">Team Management</h1>
		<div class="teams">
			<div
				v-for="team in teams"
				:key="team.name"
				class="team"
				@dragover.prevent
				@drop="onDrop($event, team)"
				@touchmove="onTouchMove($event)"
				@touchend="onTouchEnd(team)"
			>
				<h2>{{ team.name }}</h2>
				<ul>
					<li
						v-for="(member, index) in team.members"
						:key="member"
						:class="{ holding: draggedMember?.team === team && draggedMember?.index === index }"
						draggable="true"
						@dragstart="onDragStart($event, team, index)"
						@touchstart="onTouchStart($event, team, index)"
					>
						{{ member }}
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "App",
	data() {
		return {
			teams: [
				{ name: "Team A", members: ["Alice", "Bob"] },
				{ name: "Team B", members: ["Charlie", "Diana"] },
				{ name: "Team C", members: ["Eve", "Frank"] },
			],
			draggedMember: null,
			touchTargetTeam: null,
		};
	},
	methods: {
		onDragStart(event, team, index) {
			this.draggedMember = { team, index };
		},
		onTouchStart(event, team, index) {
			this.draggedMember = { team, index };
			event.target.classList.add("holding");
		},
		onTouchMove(event) {
			const touch = event.touches[0];
			const element = document.elementFromPoint(touch.clientX, touch.clientY);
			const teamElement = element.closest(".team");

			if (teamElement) {
				const teamName = teamElement.querySelector("h2").innerText;
				this.touchTargetTeam = this.teams.find((team) => team.name === teamName);
			}
		},
		onTouchEnd() {
			if (this.touchTargetTeam && this.touchTargetTeam !== this.draggedMember.team) {
				const { team: sourceTeam, index } = this.draggedMember;
				const [movedMember] = sourceTeam.members.splice(index, 1);
				this.touchTargetTeam.members.push(movedMember);
			}
			this.resetDrag();
		},
		onDrop(event, targetTeam) {
			const { team: sourceTeam, index } = this.draggedMember;
			if (sourceTeam !== targetTeam) {
				const [movedMember] = sourceTeam.members.splice(index, 1);
				targetTeam.members.push(movedMember);
			}
			this.resetDrag();
		},
		resetDrag() {
			const holdingElement = document.querySelector(".holding");
			if (holdingElement) holdingElement.classList.remove("holding");
			this.draggedMember = null;
			this.touchTargetTeam = null;
		},
	},
};
</script>

<style lang="scss">
.app {
	display: flex;
	flex-direction: column;
	align-items: center;
	font-family: Arial, sans-serif;

	.teams {
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
		gap: 1rem;

		.team {
			padding: 1rem;
			width: 150px;
			border: 1px solid #ccc;
			border-radius: 5px;
			background-color: #f9f9f9;

			h2 {
				font-size: 1.2em;
				margin-bottom: 0.5rem;
			}

			ul {
				list-style: none;
				padding: 0;

				li {
					padding: 0.5rem;
					margin-bottom: 0.3rem;
					background-color: #e0e0e0;
					border-radius: 5px;
					text-align: center;
					cursor: grab;
					transition: transform 0.2s ease, opacity 0.2s ease;

					&.holding {
						opacity: 0.7;
						transform: scale(1.05);
					}

					&:active {
						cursor: grabbing;
					}
				}
			}
		}
	}
}
</style>
