<template> 
	<footer id="globalfooter">
		<div class="description-panel">
			The Cooper Union<br v-if="mobile" /> 
			School of Art<br />
			End of the Year Show 2021 
		</div>
		<div class="nav-panel">
			<ul class="nav-list">
				<li v-for="item in items" :key="item" :class="['nav-item', isActiveRoute(item.name)]"> <router-link :to="item.path">{{item.name}}</router-link> </li>
			</ul>
		</div>
	</footer>
</template>

<script>
  import { ref, computed } from 'vue'
  import { useStore } from 'vuex'  
  import { useRoute } from 'vue-router'

  export default {
    name: 'GlobalFooter',
    props: {
      items: Array
    },
    setup(props){
      const store = useStore()
      const route = useRoute()

      //returns state for all area-nav items
      const activeGlobal = store.state.application.activeGlobal

      const isActiveRoute = (current) => {
        if(current === route.name) {
          store.commit('setGlobalNav', current)
          return 'active'
        }
        
        return undefined
      }
      
      return { isActiveRoute }
    }
  }
    
</script>

<style scoped>
	body.dark #globalfooter {
		border-top: 1px solid white;
	}
	
	#globalfooter {
		color: white;
		background-color: black;
		box-shadow: 50vw 0 0 black, -50vw 0 0 black;
		width: calc(100% - 240px);
		margin: 0 auto;
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		align-items: center;
		padding: 36px 0;
	}
	
	.description-panel {
		background-image: url(../assets/footerlogo.png);
		background-repeat: no-repeat;
		background-position: left center;
		background-size: 92px auto;
		min-height: 138px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		padding-left: 128px;
		margin-right: 48px;
		font-size: 16px;
		white-space: nowrap;
		line-height: 1.25;
	}
	
	.nav-panel {
		flex: 1;
	}
	
	.nav-panel .nav-list {
		list-style-type: none;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-around;
		font-size: 16px;
		margin: 0;
	}
	
	.nav-panel .nav-list li {
		margin: 0 1em;
	}
	
	@media screen and (min-width: 768px) and (max-width: 1024px) {
		#globalfooter {
			width: calc(100vw - 72px);
		}
	}
	
	@media screen and (max-width: 767px) {
		#globalfooter {
			width: calc(100vw - 48px);
			flex-direction: column;
			padding-bottom: 50px;
		}
		
		.description-panel {
			padding-left: 116px;
			margin-right: 0;
		}
		
		.nav-panel .nav-list {
			margin-top: 56px;
		}
	}
</style>

