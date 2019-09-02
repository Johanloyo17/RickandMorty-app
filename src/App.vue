<template>
	<v-app>
		<v-app-bar
				dark
				app
				hide-on-scroll
		>
			<v-app-bar-nav-icon></v-app-bar-nav-icon>
			<v-toolbar-title>Title</v-toolbar-title>
			<v-spacer></v-spacer>
			<div
				class="
					d-flex
					wrap
					justify-space-around
					align-center
					fill-height
				"
				>	
				<v-flex ma-3>
					<router-link to="/about">
						<v-btn flat small color="success"> 
							about
						</v-btn>
					</router-link>
				</v-flex>

				<v-flex ma-3>
				<router-link to="/">
						<v-btn flat small color="primary"> 
							home
						</v-btn>
					</router-link>
				</v-flex>
			</div>
		</v-app-bar>

		<v-content>
			<router-view/>
		</v-content>
	</v-app>
</template>

<script>

export default {
	name: 'App',
	data: () => ({
		//
	}),
};
</script>
