<template>
	<div class="app">
		<h1 :style="{ color: draggedMember ? 'red' : 'inherit' }">Team Management</h1>
		<div class="teams">
			<div
				v-for="team in teams"
				:key="team.name"
				class="team"
				@dragover.prevent
				@drop="handleDrop(team)"
				@touchmove="onTouchMove"
				@touchend="finalizeTouchMove"
			>
				<h2>{{ team.name }}</h2>
				<ul>
					<li
						v-for="(member, index) in team.members"
						:key="`${team.name}-${index}`"
						:class="{ holding: isHolding(team, index) }"
						draggable="true"
						@dragstart="startDrag(team, index)"
						@dragend="clearDragState"
						@touchstart="startDrag(team, index)"
					>
						{{ member }}
					</li>
				</ul>
			</div>
		</div>
	</div>
	<p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Delectus facilis qui mollitia illum nisi, ex quia magni velit ipsum cupiditate dolorum similique consequatur neque earum. Modi natus rerum fugit aspernatur.
	Dolore enim libero mollitia ut cum, reiciendis tenetur magni. Hic eius quidem, obcaecati excepturi cum, minus sequi repellat odit modi labore illo eaque praesentium culpa impedit minima ut. Vel, ducimus?
	Adipisci provident cum ex aperiam minima sit eligendi quo? Delectus incidunt ut similique eligendi tempora architecto eius, quis repellendus ipsam quisquam rem amet nam? Enim quas possimus expedita quibusdam accusantium!
	Obcaecati deserunt quos modi, expedita at provident voluptates soluta ratione excepturi accusamus nobis corporis sapiente repellat dignissimos architecto nihil maiores vitae. Officia, quisquam placeat. Id atque architecto vitae minima eius.
	 enim quia, alias eveniet quaerat harum sequi eligendi quos ea? Inventore sunt excepturi, quod, nobis eveniet dolores quos consectetur non eum eius repudiandae ex ducimus doloribus.</p>
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
			targetTeam: null,
		};
	},
	methods: {
		clearDragState() {
			this.draggedMember = null;
			this.targetTeam = null;
		},
		startDrag(team, index) {
			this.draggedMember = { team, index };
		},
		isHolding(team, index) {
			const { draggedMember } = this;
			return draggedMember && draggedMember.team === team && draggedMember.index === index;
		},

		onTouchMove(event) {
			const touch = event.touches[0];
			const target = document.elementFromPoint(touch.clientX, touch.clientY);
			const teamElement = target?.closest(".team");

			if (teamElement) {
				const teamName = teamElement.querySelector("h2").innerText;
				this.targetTeam = this.teams.find((team) => team.name === teamName) || null;
			} else {
				this.targetTeam = null; // Reset target if not over a team
			}
		},
		finalizeTouchMove() {
			this.transferMember(this.targetTeam);
			this.clearDragState();
		},
		handleDrop(targetTeam) {
			this.transferMember(targetTeam);
			this.clearDragState();
		},
		transferMember(targetTeam) {
			const { team: sourceTeam, index } = this.draggedMember || {};
			if (sourceTeam && targetTeam && sourceTeam !== targetTeam) {
				const movedMember = sourceTeam.members[index];

				this.teams = this.teams.map((team) => {
					if (team === sourceTeam) {
						return { ...team, members: team.members.filter((_, i) => i !== index) };
					} else if (team === targetTeam) {
						return { ...team, members: [...team.members, movedMember] };
					}
					return team;
				});
			}
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
