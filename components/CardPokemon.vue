<template>
    <div class="card">
        <div class="card-image">
            <figure>
				<img v-if="pokemon.sprites.other['official-artwork'].front_default" :src="pokemon.sprites.other['official-artwork'].front_default" :alt="pokemon.name">
            </figure>
        </div>
        <div class="card-content">
            <h3>{{ name }}</h3>
            <ul>
                <li><h4>Abilities:</h4> <span v-for="ability in pokemon.abilities" :key="ability.slot">{{ cleanOutput(ability.ability.name) }}</span></li>
                <li><h4>Types:</h4> <span v-for="type in pokemon.types" :key="type.slot">{{ cleanOutput(type.type.name) }}</span></li>
                <li><h4>HP:</h4> {{ pokemon.stats[0].base_stat }}</li>
                <li><h4>Attack:</h4> {{ pokemon.stats[1].base_stat }}</li>
                <li><h4>Defense:</h4> {{ pokemon.stats[2].base_stat }}</li>
            </ul>

			<button @click="hide = !hide">Learn more</button>
        </div>

		<div class="learnmore" :aria-hidden="hide">
			<div class="card-content">
				<button @click="hide = !hide">Close</button>
				<h3>{{ name }}</h3>
				<h4>{{ name }} is a master of <span v-for="moves in pokemon.moves.slice(0,1)" :key="moves.slot">{{ cleanOutput(moves.move.name) }}</span> and is relatively <span v-if="pokemon.stats[0].base_stat>40">strong</span><span v-else>weak</span> ({{pokemon.stats[0].base_stat}} HP).</h4>
				
				<p>Pikachu ipsum dolor sit amet squirtle poliwag nidoran rhydon. Vulpix ekans clefairy venonat magnemite.</p>

				<h4>Favorite Moves</h4>
				<ul>
					<li><span v-for="moves in pokemon.moves.slice(0,5)" :key="moves.slot"><strong>{{ cleanOutput(moves.move.name) }}</strong></span></li>
				</ul>
				
			</div>
		</div>
    </div>
</template>

<script>
export default {
    props: {
        name: String
    },
    data() {
      return {
        pokemon: [],
		image: '',
		hide: true
		}

    },
    async fetch() {
      this.pokemon = await fetch(
        'https://pokeapi.co/api/v2/pokemon/' + this.name.toLowerCase()
      ).then(res => res.json())
    },
    methods: {
        cleanOutput(string) {
            string = string.replace(/-/g, ' ')    
            const words = string.split(" ");

            for (let i = 0; i < words.length; i++) {
                words[i] = words[i][0].toUpperCase() + words[i].substr(1);
            }

            string = words.join(" ");

            return string
        }
    }
}
</script>

<style lang="scss" scoped>

.card {
	overflow: hidden;
}

.card-image {
	background: #E0E0E0;
	

	figure {
		aspect-ratio: 37/29;
	}

	img {
		object-fit: contain;
		width: 100%;
		height: 100%;
	}
}

h3 {
    font-size: 24px;
    font-weight: 900;
    line-height: 28px;
    margin-bottom: 12px;
    color: #000;
}

h4 {
    display: inline-block;
    font-weight: 600;
}

li {
    font-size: 14px;
    color: #000;

    span {
        &:after {
            content: ', ';
        }

        &:last-child:after {
            content: '';
        }
    }
}

button, a {
	color: #5700FF;
	border: 0;
	border-radius: 999vw;
	font-size: 14px;
	box-shadow: 0 0 0 2px #5700FF;
	background: none;
	padding: 12px 24px;
	margin-top: 20px;
	transition: all 0.2s ease-in-out;
	cursor: pointer;

	&:hover, &:focus {
		background: #5700FF;
		color: #fff;
	}
	
}

.learnmore {
	position: absolute;
	top: 0;
	left: 0;
	height: 100%;
	width: 100%;
	background: #5700FF;
	color: #fff;
	transition: all .2s ease-in-out;

	&[aria-hidden=true]{
		transform: translateY(100%);
	}
	
	* {
		color: #fff;
	}

	h4 {
		font-size: 18px;
		font-weight: 600;
	}

	p {
		margin-bottom: 1.5em;
	}


	button {
		position: absolute;
		top: 0;
		right: 20px;
		padding: 0;
		box-shadow: none;
		text-transform: uppercase;
		font-size: 12px;
		font-weight: 900;
		color: #fff;

		&:hover, &:focus {
			background: none;
			color: #fff;
			opacity: .7;
		}
	}
}
</style>