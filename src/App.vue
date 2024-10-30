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
	Facilis eos, libero, fugit illum repellat quasi voluptas sit sed optio ipsa, blanditiis accusamus! Voluptatibus deleniti, iusto neque qui explicabo quia quos, fuga quas quidem quaerat ratione repellat alias laborum?
	Vitae quas esse, nulla obcaecati facilis dicta, cupiditate minima deleniti perspiciatis placeat hic quod. Ad nam ipsum quisquam, consequuntur natus dolores minus inventore officia at, error illum dolorem? Vel, asperiores.
	Consequatur quo dignissimos repellat amet voluptate laboriosam nemo, vitae culpa. Nostrum molestias illo modi, cupiditate vel, iste, reiciendis similique laudantium sit itaque facilis ab nihil voluptatibus? Iure, illo ullam! Laboriosam.
	Ducimus quisquam pariatur vitae ea doloribus quod delectus minima praesentium voluptatibus quidem eaque, itaque libero, culpa reprehenderit distinctio? Nulla quis architecto omnis temporibus pariatur numquam aperiam error ducimus sapiente magnam!
	Explicabo, repellendus error. Numquam sunt nisi aut at quia, iusto dicta cum fuga tenetur impedit rerum architecto quisquam explicabo. Sed fugiat corrupti voluptatibus voluptatem tenetur officiis rem laudantium esse illum.
	Non delectus, eaque debitis dolorum dicta, facere modi rerum obcaecati iusto velit ipsum itaque nisi error numquam possimus nostrum, sunt perspiciatis. Nihil sed omnis unde tempora ea aliquam saepe illo.
	Iure libero rerum neque minima! Alias nostrum earum asperiores atque enim impedit, voluptatem autem et consectetur rem eum repudiandae eveniet placeat nesciunt repellat molestiae ipsa adipisci natus voluptate quidem. Sed.
	Nesciunt, aspernatur deserunt. At earum sit delectus dolores doloribus, doloremque nesciunt impedit ad nihil unde obcaecati distinctio in praesentium magnam eligendi, consequuntur, maiores laborum aspernatur consectetur pariatur odio quia. Fuga.
	Neque, quasi quas deleniti unde sint vitae quisquam maiores mollitia saepe excepturi ratione doloremque omnis natus voluptates laudantium adipisci aut reprehenderit quibusdam! Aliquid animi expedita minima eius porro esse accusantium?
	Adipisci cumque sunt iusto a quas perferendis fuga quae at similique? Quidem distinctio animi fugit, earum dolorem saepe sunt omnis ex nobis deleniti maxime quos vitae debitis, accusamus officia nemo.
	Rem, tempore quasi possimus similique maxime officiis a rerum perspiciatis nesciunt ducimus omnis minus fugit expedita quae consequuntur eum cumque repudiandae tenetur, debitis iusto ad aspernatur voluptatum cupiditate optio. Tenetur?
	Dicta delectus sint distinctio incidunt cum, reprehenderit excepturi ipsum recusandae. Libero voluptatibus vero eum soluta commodi aperiam. Quibusdam, exercitationem adipisci autem, repellendus ipsum cupiditate doloribus aliquam animi, sunt culpa ut?
	Optio perspiciatis recusandae rerum quibusdam rem beatae tenetur, minus assumenda hic nulla velit voluptate aut, fugit at, laudantium ipsum maiores! Soluta veritatis illum repellat facere quisquam, nobis quo odit praesentium.
	Minima vel nam illum, animi reiciendis cum eligendi iure voluptas laborum accusamus perferendis, numquam architecto, nihil voluptatibus nesciunt veritatis? Suscipit consequuntur voluptatibus labore possimus sed eius architecto fuga necessitatibus exercitationem!
	Sed, voluptates eaque! Libero, modi quas perferendis expedita animi aspernatur sunt debitis molestiae assumenda magni ipsam neque asperiores! Dignissimos nostrum maiores porro minus nam! In enim impedit perferendis voluptatibus sit.
	Accusamus, voluptas, assumenda distinctio blanditiis odit natus itaque est, nisi dignissimos molestiae magnam officiis delectus cumque recusandae fuga architecto quasi nihil enim eos. Expedita exercitationem, nisi tenetur laudantium ratione voluptatibus.
	Labore ut, totam ea repudiandae nam sunt consequuntur iusto quas maxime molestiae architecto in. Debitis eveniet non voluptas voluptatum perspiciatis atque fugit ut reprehenderit, numquam explicabo at consequuntur excepturi sed?
	Odit neque excepturi a ut dicta perferendis ipsum quia odio incidunt cumque quisquam aspernatur fuga maxime ipsam reprehenderit saepe, quod sint distinctio labore magnam quis. Pariatur voluptatibus consequuntur nisi corrupti!
	Eaque eius corrupti, delectus doloremque illum vitae, doloribus modi perspiciatis fugit totam id libero impedit tempora? Maxime, porro dolores incidunt eum, dolor tempora dicta fuga voluptatem iure, possimus nostrum dolore.
	Tempora quibusdam officia ducimus nobis voluptate ullam magnam, deleniti eos vitae, maiores, ipsam harum assumenda at voluptatibus dignissimos velit nulla neque odit dolor unde odio beatae iure adipisci. Tempore, iure?
	Dolorem neque repellat laborum impedit ducimus molestias expedita ut ab facere exercitationem, temporibus doloremque nemo culpa! Autem nam sint debitis quidem? Recusandae sint eaque reprehenderit iste tempore cum, assumenda explicabo.
	Vero esse quo delectus soluta quisquam! Animi mollitia ipsum quisquam quod inventore aliquid sit aspernatur. Adipisci expedita, velit modi excepturi voluptatum nobis veniam similique culpa debitis quia totam. Excepturi, facere!
	Ducimus, possimus aperiam vero temporibus dignissimos, culpa modi quisquam non ut quibusdam aliquid. Quis in voluptas modi impedit dolorem minima quibusdam quasi dicta numquam fuga id exercitationem, laborum magnam nobis.
	Ipsum architecto et ab expedita nihil, quia cumque velit, ducimus quis perspiciatis dignissimos repellendus! Laborum aspernatur repellendus corporis ipsum odio optio dolore quaerat beatae suscipit, nobis maxime unde obcaecati qui?
	Pariatur voluptas, corrupti optio illo iste earum ipsum consequatur ducimus reiciendis in assumenda! Molestias ex sint debitis, fuga repellendus iure minus accusantium ipsam. Quisquam laudantium corporis fugit eveniet, molestiae accusantium.
	Quae tempore numquam laboriosam vel totam vitae error saepe omnis. Incidunt nesciunt cum reiciendis animi iure quia alias beatae debitis? Ducimus quisquam asperiores sint fugit quaerat accusantium perspiciatis, dolorem pariatur.
	Magnam assumenda sit nam vitae, aut illo! Quia reiciendis nisi ad quae nemo corrupti, dolores est. Veniam tempora temporibus dolorem perspiciatis optio quasi ut quaerat itaque, aperiam saepe fugiat architecto?
	Quisquam quibusdam accusantium neque ullam labore, placeat alias facere? Quae consectetur ea vero veniam maiores voluptatum esse neque voluptate? Nulla ipsam, reprehenderit dolores numquam a ex voluptate quis autem libero?
	Necessitatibus magni placeat ullam velit aliquam commodi tempore dolorum et eum, eaque, id vero quibusdam expedita ad repudiandae iusto veritatis exercitationem itaque dignissimos facere, tenetur modi dolore assumenda! Laboriosam, debitis?
	Dolorum illo soluta a laudantium voluptas, aliquid quia, autem blanditiis id iure numquam eum temporibus explicabo obcaecati necessitatibus, fugiat ipsam aut molestias? Officia earum commodi, ex corrupti molestiae porro eum.
	Deleniti maiores quidem fugiat accusantium quaerat ipsam ipsa qui voluptas fuga modi, quod repellendus debitis non id tempora praesentium? Provident hic quod ipsum fuga sapiente officiis repudiandae cumque facilis perspiciatis!
	Est amet voluptatem delectus illum in dolores minus quasi? Maiores temporibus odio neque. Voluptatem rerum deleniti molestiae dolorem natus accusamus? Animi rerum quisquam commodi dolorum pariatur? Excepturi porro quis pariatur.
	Quod praesentium obcaecati sed vel, reprehenderit aliquam eaque ipsa excepturi modi, dolorum illum distinctio hic ratione quas pariatur corrupti eum, iure molestiae et! Excepturi, asperiores in aliquam perferendis fuga dolore.
	At deleniti adipisci porro. Repudiandae, repellat tempore. A in aliquid tempore sapiente delectus voluptatem cumque sequi molestiae nulla inventore est veritatis rem quibusdam sit non praesentium deleniti quasi, impedit numquam?
	Illum neque nostrum consequuntur qui earum numquam ducimus quibusdam nihil nobis consectetur eaque sequi eligendi ea aspernatur hic sunt vitae libero consequatur harum architecto sapiente voluptatibus eum, quas atque! Veritatis.
	Iure, quisquam est illo fuga voluptatem maiores in quas fugit numquam voluptate nostrum sed, ipsam dolor placeat delectus facilis soluta sunt! Eius deleniti possimus non. Reiciendis iusto modi explicabo iure.
	Nobis aliquid rerum recusandae sint, hic modi amet ad ipsum dignissimos nesciunt aperiam voluptate mollitia atque eius perspiciatis necessitatibus voluptas quo reprehenderit exercitationem voluptatibus dolores in aspernatur. Modi, culpa temporibus?
	Ducimus eveniet illo molestias quidem, saepe omnis commodi incidunt, consectetur, molestiae maxime vitae deleniti officia assumenda laborum optio. Ratione pariatur numquam nisi dignissimos asperiores perspiciatis culpa ducimus veritatis soluta esse.
	Labore atque sed dolorum eveniet eligendi quas cum dicta assumenda nesciunt! Modi odit quo laborum. Eligendi nihil, incidunt voluptatibus fugit impedit tenetur perferendis laboriosam omnis veritatis, tempora similique libero voluptatum!
	Ab consectetur quisquam dignissimos autem asperiores. Autem quod, hic impedit nobis consectetur maxime laudantium asperiores velit tempora deserunt quaerat culpa animi nam voluptate excepturi aliquid laborum ex labore reiciendis. Provident.
	Perferendis illum deleniti tenetur? Commodi eligendi, error aliquid explicabo deleniti asperiores nesciunt modi vel maxime dolorem magni corporis facilis perferendis obcaecati laudantium, eum laboriosam repudiandae! Optio eligendi error ipsam velit!
	Sunt asperiores quia quas, dolorem pariatur, corrupti porro voluptatibus accusantium nam nulla aliquid voluptatem suscipit eligendi distinctio iusto tempora atque! Molestiae cupiditate beatae harum architecto dolore totam sunt expedita suscipit?
	Mollitia iusto illo fuga. Asperiores voluptatem adipisci eum, deleniti soluta iure dolorem in ea at sapiente necessitatibus maxime. Minima quos quisquam facere doloribus id molestias facilis sed vitae odit voluptate.
	Illo quisquam harum libero labore omnis, delectus quasi a facilis laudantium temporibus incidunt nam dolor reiciendis repellat? Deserunt delectus fugiat natus, perspiciatis maxime blanditiis molestiae consequuntur, distinctio a nemo sequi!
	Nemo suscipit numquam minus repudiandae fuga facere corporis ipsam! Dolorem veniam magni veritatis tenetur corrupti, molestiae eius consequuntur placeat earum doloribus in quia suscipit velit iusto dolore cumque culpa distinctio.
	Voluptas soluta illum alias delectus totam vero odit, eaque repudiandae labore a laborum rerum magni reprehenderit cumque perspiciatis quasi blanditiis aliquid facere fuga nesciunt? Corrupti possimus illo est doloremque ullam.
	Labore ipsa fugit, quasi quam voluptate, quidem iusto placeat aliquam hic repellendus voluptates at rerum in sequi nemo! Dolorem, quaerat laboriosam rerum odio nesciunt hic tempore. Velit reprehenderit ex maiores?
	Odit itaque animi harum, iusto dolores explicabo quo doloribus officiis quidem aut placeat quibusdam pariatur incidunt. Tempora accusantium sed magni cupiditate hic soluta dolorem explicabo, inventore aspernatur maxime eveniet nisi.
	Molestiae quas tenetur eligendi beatae maiores earum odio eaque sit exercitationem accusantium corrupti quia error ab, aperiam quidem repudiandae. Laboriosam explicabo cum necessitatibus quidem facere magnam alias eaque asperiores labore.
	Sint tenetur blanditiis quos libero veritatis qui eius repellat doloribus, optio, officiis excepturi eaque. Aut soluta earum, similique, dignissimos vel quaerat explicabo repudiandae nobis ratione, dolores assumenda eaque amet molestias.
	Quam quos quis in distinctio, animi voluptate eligendi eum. Dolorum, doloribus reiciendis. Praesentium inventore quisquam quaerat eos temporibus autem, totam omnis officiis sit accusamus? Sed possimus placeat libero rem? Saepe?
	Voluptate voluptatum culpa incidunt optio officia doloremque laboriosam sint. Beatae quas nulla tenetur nostrum? Saepe eos provident exercitationem necessitatibus natus dignissimos qui inventore rem iste tempore! Beatae nam incidunt ipsa.
	Sed, ab ea alias ipsam, laudantium reiciendis deserunt ullam accusantium corporis dolores, sint omnis ad nam? Minima, excepturi illum saepe praesentium repellendus voluptatem suscipit, debitis nemo, adipisci atque corporis! Porro.
	Non eum porro repudiandae in saepe possimus debitis, inventore facere deserunt consequuntur illo quos quaerat? Quam fugiat quia at ipsa quos necessitatibus adipisci ut hic culpa? Tempore, aspernatur modi. Recusandae.
	Reprehenderit eligendi consequatur et voluptate quisquam similique at rem aliquam ex hic quasi quibusdam earum sequi amet esse molestias consequuntur placeat, praesentium voluptatum dolore enim porro vitae commodi. Harum, laborum.
	Voluptatem provident quaerat similique esse vero reiciendis, porro repudiandae ducimus ad facere in sint incidunt! Maxime nostrum necessitatibus, at nobis voluptates laboriosam, architecto vero culpa recusandae quod quasi quia reprehenderit.
	Odit consequatur dicta sed doloremque nam mollitia laborum, ducimus autem sequi atque excepturi officiis blanditiis aliquid accusantium, pariatur ex facilis nemo repellat iure! Sapiente molestias, error blanditiis necessitatibus voluptates aliquid?
	Iste iure similique minima alias harum. Atque consequatur incidunt fugiat architecto non fugit, quod reiciendis totam necessitatibus quidem culpa, vitae harum vero dolor iusto voluptatem quos dignissimos quaerat ab porro.
	Expedita praesentium omnis rerum in voluptates ipsa, adipisci, nobis, quis voluptatibus tempora atque cumque cum blanditiis. Neque nulla distinctio minus, ea tenetur, id adipisci hic laborum esse temporibus vero porro.
	Vel iste vero, rerum ducimus a quas dolorem aspernatur enim eos tenetur accusamus ipsum. Odit corrupti reiciendis autem ipsum earum dolores est, ipsa, consequuntur debitis iure vitae cupiditate animi unde.
	Quidem officia cum ut earum! Ducimus fugiat ut atque aspernatur quasi dolor reiciendis temporibus illo expedita, quis quia totam iusto rem fuga autem suscipit tempora quidem non nemo laudantium? Illum.
	Aspernatur, animi! Obcaecati iusto, illum possimus magni exercitationem eum impedit dolore itaque dolores ipsam non minima explicabo magnam autem totam quae eveniet omnis est quisquam facilis veritatis atque sit. Et.
	Adipisci cupiditate eligendi ipsa quibusdam necessitatibus, officiis fuga hic quasi labore obcaecati reiciendis odit saepe a quos voluptatibus tempora excepturi iusto quisquam tempore minima accusantium, minus illum quidem? Alias, temporibus.
	Sed officia nulla eveniet eos nihil sunt quasi a exercitationem consequatur quisquam quam cumque consequuntur saepe consectetur omnis porro labore minus architecto atque quos dolores, accusamus minima mollitia? Quisquam, laborum!
	Tempora ad quos quasi eos minus officiis repellendus doloremque repudiandae eaque ipsa quibusdam dolorum optio commodi quo, officia expedita praesentium reprehenderit debitis aliquam dicta amet reiciendis incidunt dolores? Eos, eius.
	Ducimus ex quisquam dicta nulla quas velit labore? Nam ullam sed porro itaque saepe error exercitationem fugit fugiat amet ea illo illum repellat quam dolorem vitae, voluptatum perferendis nihil ipsum?
	Minus sunt facilis commodi doloribus doloremque dolorem repellat assumenda laborum reiciendis distinctio illum nulla nobis cupiditate voluptate in sit, quasi blanditiis fuga saepe optio qui, ad dolores? Provident, et perspiciatis.
	Ad neque reiciendis voluptatum impedit dolorem quam placeat provident mollitia nihil debitis, vero illum dolorum et beatae deserunt molestiae eum ducimus vitae corporis dicta architecto ex tempora ipsa explicabo. Aut!
	Vitae, veritatis illum itaque officiis tenetur magnam? Suscipit quisquam tempora quia dicta voluptas. Natus quisquam impedit aspernatur pariatur explicabo saepe, excepturi veniam totam, et error tempora recusandae fuga quibusdam ipsam.
	Aut odit doloribus rerum. Laborum est molestiae dolorum itaque porro quo provident atque cumque rem maxime, molestias nam, eveniet dignissimos expedita dolor accusantium distinctio veniam iusto sed doloremque! Doloribus, illum.
	Ut, ratione vel. Eligendi blanditiis quaerat aperiam at qui quia error. Earum, facilis ducimus saepe voluptatum inventore commodi, repudiandae, facere fugiat amet eligendi suscipit cum esse deserunt laudantium. Deleniti, blanditiis?
	Nesciunt pariatur, quod magnam ea, impedit, neque iure eius harum expedita delectus ad quasi suscipit perferendis optio officia quia vero cum adipisci! Quod deserunt ut exercitationem iusto explicabo, sed veritatis.
	Consequatur sed eligendi fuga quaerat magnam sit quod ab assumenda nam vel dolorem dolor facilis, illum molestias doloremque consequuntur sunt libero sequi esse dolorum. Veniam, adipisci. Dolorem quas perferendis ipsum.
	Dignissimos assumenda officia in! Beatae quos modi aspernatur saepe, quo iusto suscipit atque voluptates, repellat iste corrupti similique est libero architecto inventore? Excepturi et dolores consequuntur incidunt illo laboriosam eum.
	Obcaecati et maxime suscipit dolores quos laborum facilis nobis veniam iure, natus dolor autem mollitia nisi nulla omnis veritatis voluptate voluptas voluptatibus sed ipsa. Facilis dolorum aut praesentium culpa in!
	Quis, doloremque? Omnis, optio quo! Dicta dolorem architecto facilis? Harum cumque dolores aliquam totam, nihil nesciunt quaerat deserunt ducimus ipsam nostrum eaque possimus quos est iure pariatur unde autem repellat.
	Culpa, eius consequuntur corrupti animi ab, nulla maxime ipsum mollitia, nostrum pariatur autem assumenda placeat voluptas! Dignissimos neque itaque accusamus ratione, alias laboriosam placeat numquam omnis aspernatur ut error velit.
	Consequuntur necessitatibus perspiciatis doloribus! Hic, inventore. Dolore ipsa dicta velit numquam, ab beatae labore officiis eveniet deleniti aut quos tenetur consequatur ex eius eligendi incidunt iste omnis quod rem nam!
	Consectetur, dolor maiores ratione pariatur optio voluptatem fuga quisquam quo eaque, nisi perferendis fugiat quaerat laboriosam corporis! Dolor dolore tempore assumenda necessitatibus dolorem velit enim corrupti, doloremque laudantium. Pariatur, omnis!
	Nemo, eius! Similique tempore corporis accusamus commodi maiores dolores necessitatibus laborum, alias quisquam impedit, aut, quam quos mollitia vel veritatis perferendis. Sint labore nobis tenetur error, incidunt minus doloribus recusandae!
	Iste voluptate consequuntur dolorem commodi, quam dolorum dolores facere perferendis culpa nisi vel. Reprehenderit, natus aperiam harum tenetur sunt praesentium impedit perferendis quasi, maiores veritatis, tempora blanditiis laudantium maxime animi!
	Ratione dicta minus tempore et deserunt. Fugiat voluptatem architecto facilis maiores consequuntur omnis ut. Odit, aliquam id. Unde quas nostrum, quam possimus a reprehenderit ipsa illo ipsum facilis, quaerat sapiente!
	Dolor nisi eius ex officia. Dignissimos eius, repellat quas debitis ratione tempore, veritatis nihil esse deserunt similique rem. Hic amet repellat quod excepturi vel quos unde ea mollitia earum repudiandae?
	Quasi dolorem ipsum vitae numquam expedita, deleniti, vero ullam aliquid eum delectus, animi dolorum odio omnis accusantium quae ratione fuga sit mollitia! Soluta, obcaecati? Nobis itaque quo assumenda ea eaque!
	Ullam officia ipsam distinctio tempora dolor perferendis nihil, omnis autem, ipsa assumenda sunt itaque, suscipit porro voluptatibus quo adipisci ad rerum reprehenderit ipsum harum! Ipsum dolores vel autem culpa consequuntur!
	Nulla, officia. Corrupti maxime saepe eveniet officiis quibusdam veritatis rerum eius dolore fuga ab laborum adipisci dolorum assumenda vel ducimus accusamus, voluptatem nostrum minus. Sed doloribus non sunt tenetur quos!
	Maiores, veniam. Ut ab, atque quam iste aut odit sed ipsum, repellat possimus similique commodi quae deserunt porro, incidunt veniam reiciendis nostrum totam consequatur dolorem? Alias saepe iusto voluptas ex.
	Quo aut earum ex maiores sed, facere quas at esse voluptatem aperiam exercitationem illo suscipit repudiandae id nam ab enim dolor vero, aliquid vitae ullam iusto. Non id ex ut?
	Deleniti id nesciunt corrupti amet asperiores? Quia doloribus, provident officiis, tempore, quibusdam repellendus dolorem modi repudiandae nemo a cupiditate. Provident vero nulla excepturi molestiae saepe magnam voluptatem sequi dolor tenetur.
	Delectus animi totam soluta culpa, dolorem atque mollitia nesciunt deleniti architecto ducimus eos consequuntur accusantium officia autem incidunt iusto nulla obcaecati velit tempore consectetur a et. Nobis blanditiis numquam beatae.
	Officiis quibusdam nobis impedit quia repellat cupiditate, aliquam voluptatum facere, neque, laborum doloribus at sint! Veritatis facere, vero eveniet beatae inventore illum impedit odit quidem alias deserunt voluptatibus sed tenetur.
	Minima perspiciatis, ullam labore sed dolorem ipsam eum ducimus officia eveniet sequi eaque saepe nesciunt odit, fugit vitae nulla architecto quaerat ipsum. Itaque enim eveniet maiores facilis quasi cumque aut?
	Soluta voluptates doloribus molestias reprehenderit. Aliquid praesentium quisquam accusantium laudantium tenetur aperiam obcaecati repellat rerum nostrum molestiae voluptatem officia exercitationem dolor odio quos quibusdam corrupti veniam, error mollitia earum dolorem.
	Exercitationem nam a repellendus accusantium voluptatem et totam! Libero voluptas maiores quibusdam sequi. Accusamus odio quas incidunt asperiores delectus, maxime, fugiat dolore eum debitis quaerat assumenda iusto iure placeat? Inventore!
	Fuga, in error? Quos molestias quibusdam nesciunt ab. Rerum, provident et! Expedita qui, rerum, consequatur pariatur consequuntur laborum cupiditate ipsa laudantium placeat sunt nulla voluptas blanditiis quod deleniti. Ducimus, ex?
	Doloremque tempora quam explicabo corporis neque animi reiciendis, dolorum, ut ex ducimus officia minus. Velit a corporis sed minus nemo exercitationem quae quam animi odit aliquam consequuntur, assumenda dolor dignissimos!
	Laboriosam atque assumenda porro eum sint nemo incidunt tempora id quam. Magnam molestiae asperiores sint quia? Optio quidem enim iure veniam rerum. Cupiditate facere quia sapiente natus aliquam ratione. Suscipit.
	Incidunt blanditiis numquam quas, iusto tempore labore dolorum. Reprehenderit, non doloremque veritatis inventore temporibus suscipit voluptatem tempore quidem laboriosam, cumque optio ex ipsa ducimus quod itaque, eveniet vel ab ratione?
	Illo officia, ab quasi dignissimos voluptatum error autem perspiciatis consequuntur voluptatem eius nihil voluptates dolores, necessitatibus nesciunt facere natus iste numquam iusto ipsum molestias, assumenda saepe. Vitae obcaecati dolorum necessitatibus!
	Nobis doloribus error deserunt ea, exercitationem quibusdam, quidem recusandae ipsa voluptates minus expedita eveniet facilis, ab natus et perspiciatis aperiam corporis. Consectetur autem blanditiis itaque, dolore iusto ratione perferendis laborum!
	Officiis hic ipsum veritatis, in at sit laborum inventore iusto tempore quos libero qui officia totam, nihil mollitia omnis! Maiores odio facere repellendus. Quis quos vitae temporibus excepturi repudiandae non?
	Necessitatibus dolorum quos nesciunt nemo quia accusamus itaque dolor porro pariatur magni quod ipsam ab iusto, eum in nulla tenetur. Assumenda nam, repudiandae eligendi sed dignissimos quam harum blanditiis cupiditate?
	Maiores autem possimus ratione nesciunt asperiores nemo? Unde ea autem neque recusandae tempore veritatis nostrum similique odit assumenda fugit, error dolorum aliquam quasi omnis odio veniam laborum dicta quas ullam.
	Deleniti error perspiciatis distinctio reiciendis dolores nesciunt accusamus impedit, laudantium, asperiores, inventore non omnis. Reprehenderit quas iusto ab voluptates! Necessitatibus consectetur numquam veniam iusto ipsa dolor ea temporibus quos eum.
	Doloribus, porro sequi laboriosam eum dolore fugit reprehenderit itaque doloremque dolorem repudiandae unde nostrum blanditiis. Deleniti ab, officia eos voluptatem ullam repudiandae aut a quam, aliquam aperiam fugiat temporibus praesentium?
	Dolorum adipisci, laboriosam, amet labore, voluptatem assumenda unde iure sint aspernatur pariatur harum perspiciatis magni ea fugit voluptates! Ipsum tenetur possimus nulla sapiente facere et consequuntur dicta beatae ex quo.
	Consequatur vero sed laborum perspiciatis quo consequuntur, eaque quas, unde repellat qui labore! Itaque aperiam magni suscipit dolores! Animi ullam magni asperiores, consequuntur fugiat fuga atque excepturi ea autem amet!
	Nam voluptatum inventore laborum laboriosam accusantium exercitationem nostrum neque culpa fuga omnis consequuntur alias officia, esse quasi obcaecati modi quidem quas voluptatibus doloremque. Quam laudantium laboriosam voluptatem. Quidem, autem itaque?
	Nisi inventore dolores expedita nihil iusto deleniti voluptatem neque, ipsum sed quas dolore commodi, beatae obcaecati iste cumque qui excepturi corrupti, autem eius nam atque! Itaque doloribus cum blanditiis mollitia?
	Adipisci voluptas officia ipsam non dolorem blanditiis. Consequatur, ducimus quibusdam dolores explicabo eaque, qui excepturi quis eveniet dignissimos, facilis ipsa. Omnis illo ab amet. Maxime, repellendus nemo! Eius, architecto ullam.
	Corporis, omnis est, cumque, nesciunt perspiciatis deserunt ab libero modi hic dolorem exercitationem doloribus placeat. Itaque architecto repudiandae ex eligendi! Quasi sequi eum vero nemo harum rem natus repudiandae quibusdam.
	Error culpa natus reiciendis praesentium cumque ducimus. Consequatur, accusamus officiis. Ratione odit nisi quibusdam error iure ea necessitatibus, dolorem, ad cum rem earum suscipit quasi assumenda reprehenderit consequatur voluptatibus distinctio.
	Ratione hic aliquam expedita eum repellat ipsam perspiciatis nesciunt, alias necessitatibus sed eius assumenda deleniti fuga reprehenderit velit tenetur ex aperiam tempora provident adipisci inventore? Ipsum natus explicabo nobis at.
	Consectetur dolor dignissimos minus, tempora quisquam architecto expedita praesentium quasi possimus culpa ratione quos, ducimus vitae aliquam sit corporis sint? Saepe nostrum placeat voluptatibus a officia vel autem, rem ipsam!
	Debitis cupiditate quasi molestiae, recusandae quod dicta vel at, ab commodi, enim sit officia deleniti incidunt cumque sed blanditiis hic tempore veritatis quaerat expedita a atque eius voluptatem illo! Odio?
	Repudiandae, aut libero ullam tenetur eaque blanditiis quam optio dignissimos obcaecati odio sed facere quis deleniti harum nam quaerat dolorum quod quasi impedit eligendi inventore molestiae sunt error! Vel, itaque?
	Quas ad facilis eveniet officia voluptatibus, ab ex. Expedita aspernatur assumenda modi et, autem placeat explicabo culpa ad laborum dolore, numquam possimus, incidunt ipsa nesciunt quasi nam aliquid distinctio debitis.
	Cum id sequi ea dolore accusamus voluptatibus repellat, quasi quas quod delectus incidunt eaque architecto quam quisquam tempore, voluptates exercitationem enim! Nam tempora incidunt optio voluptatum fugit veritatis explicabo? Minima.
	Maxime, odio iusto omnis numquam cum asperiores ab ad repellat obcaecati qui facilis tempora, quibusdam quidem, praesentium cupiditate vel culpa laudantium laboriosam fugit? Deleniti reprehenderit, rerum iste accusamus minus maiores!
	Ab numquam maiores beatae adipisci omnis laudantium iure nesciunt ullam et aut non possimus sit obcaecati, tempora, eum suscipit commodi maxime assumenda nostrum neque consequatur minus necessitatibus impedit! Sequi, atque.
	Omnis iure beatae esse in voluptate nulla, perferendis accusamus similique est molestiae cumque amet porro saepe facilis libero, sit debitis? Doloribus qui corporis facilis corrupti possimus vel incidunt voluptates odit.
	Sapiente, consequatur ex. Autem natus, at incidunt saepe necessitatibus nesciunt dolorum qui dicta debitis corporis ex cupiditate sapiente neque ea rem facere cumque odio quam expedita provident commodi fugiat eaque.
	Velit suscipit autem porro, illum ipsum reiciendis cum expedita nobis corrupti architecto tempora reprehenderit eligendi minima id eos enim repudiandae totam quis, nostrum veritatis saepe? Voluptate aliquid accusantium ipsa voluptas?
	Doloribus nobis fugit iusto a repellat possimus obcaecati quasi deserunt. Dignissimos placeat consequatur voluptatibus. Sapiente modi quas natus doloribus provident recusandae esse sunt deleniti. Odit amet repudiandae ea quibusdam doloremque?
	Velit vel eos quasi. Eius adipisci dolorum totam molestiae tempore! Excepturi optio nisi porro vitae labore magnam itaque obcaecati sapiente! Rerum, excepturi laboriosam hic veritatis maiores sequi. Minus, pariatur. Consequatur.
	Ut voluptatem inventore ipsam architecto consequatur enim aut pariatur voluptates, sunt blanditiis tenetur adipisci vero quo voluptatum suscipit, exercitationem veritatis incidunt molestiae tempore quasi deserunt? Facilis dolor quas voluptas provident.
	Praesentium itaque nemo cum iusto eaque necessitatibus similique ipsa porro aut, minus ex beatae dolore nisi odio fuga, facilis a! Dolor perferendis quibusdam blanditiis at illum explicabo obcaecati libero dolores.
	Dolorem, doloribus assumenda quia aliquam, hic aperiam commodi eaque doloremque magni minima quisquam inventore similique a suscipit molestiae ullam odit vero error voluptatum id odio obcaecati dolorum sequi! Nostrum, culpa.
	Ea, magnam ducimus. Enim, neque dolore possimus similique iusto ratione, iste cum ab vitae, at maiores fuga. Soluta similique animi vero reiciendis voluptate nam, commodi suscipit ipsa, asperiores, nobis est.
	Tempora eos asperiores ex explicabo doloribus debitis vero delectus quo placeat ipsum nostrum id, sequi ipsam dignissimos soluta facilis in sint officiis facere incidunt repellendus praesentium inventore? Molestias, consectetur porro.
	Qui reiciendis quam doloremque iusto quidem dicta voluptate. Corporis saepe tempora maiores tempore perspiciatis voluptatum animi, libero explicabo. Animi quidem magni libero enim ab aperiam sapiente. Aut totam nulla sunt?
	Non eligendi laborum dolore assumenda molestias quia officia atque est consequatur quas veritatis eveniet esse quis asperiores tempore debitis, maiores ducimus aliquid consectetur sequi! Harum iure eius voluptatibus fuga asperiores?
	Consectetur assumenda rerum quisquam nostrum, cumque quasi tempora earum recusandae ab corporis doloribus, mollitia odio error, nemo eum. Earum enim veniam doloremque repudiandae delectus! Maiores quos dicta nam quaerat quia.
	Labore at quo aperiam veritatis quidem nulla aliquid pariatur, unde accusamus illo perspiciatis commodi assumenda reprehenderit vel consectetur voluptate beatae repudiandae repellendus ex magnam asperiores voluptatibus odit eos culpa? Atque?
	Officia et, provident commodi illum nulla odio modi quae mollitia voluptatum, consequatur expedita libero aperiam quaerat explicabo asperiores deserunt similique, temporibus numquam nesciunt obcaecati omnis maiores quia? Perspiciatis, dolores illo.
	Nulla nemo quidem at a qui facilis animi, voluptatem inventore totam repudiandae magni ipsum temporibus tenetur odit! Eum sapiente necessitatibus corporis ratione excepturi dolorem aspernatur ducimus! A accusantium voluptatibus consequuntur!
	Enim voluptate magni aspernatur perspiciatis quo accusamus dolores reiciendis sapiente eveniet exercitationem, harum id et cumque rem eos totam voluptates, placeat minus assumenda error soluta esse praesentium. Sit, incidunt temporibus!
	Dolore quidem reiciendis nisi ipsa. Corporis dolorem recusandae eius distinctio facere similique officia adipisci nisi consequatur doloribus corrupti laudantium mollitia eos quae sint sapiente unde quibusdam, nesciunt veniam fuga aspernatur.
	Expedita veniam ipsa vero, saepe aliquid doloremque dolor quidem fugiat error aspernatur! Error nesciunt totam consequuntur sint dignissimos maiores, repudiandae porro beatae quos veniam libero repellat dicta fugiat eveniet sed!
	Ab iure, sed magnam dolore, facilis ullam alias magni accusamus nam saepe, iste id atque repellat eum quis? Nam nihil porro nostrum! Soluta asperiores alias at doloremque voluptatibus, temporibus nam.
	Perspiciatis, dolorem esse. Vero nihil temporibus neque delectus voluptates laudantium provident maiores id ipsa, eaque consequatur, voluptate iure magnam similique ullam est dolores rerum commodi quis ea iste corrupti dolor!
	Quod libero illo illum delectus est quisquam vel deserunt nemo optio tempore aspernatur, unde facere? Deserunt soluta molestiae, saepe laboriosam non sed dolorem mollitia harum itaque similique. A, fugit sequi?
	Tempore quos natus dolorem vero numquam ratione quaerat. Laboriosam assumenda cupiditate repudiandae reiciendis enim consequuntur quia quisquam itaque ipsa, beatae perferendis sit ea similique aspernatur, suscipit ullam veniam hic corrupti.
	Debitis praesentium dignissimos blanditiis iusto dolores quae veniam sunt sequi expedita molestias vero ratione error aliquid, id fuga impedit ut quasi! Debitis dolorem non aliquid, omnis expedita perferendis cumque voluptas.
	Nulla eius labore, fugiat similique distinctio quos aspernatur voluptatibus asperiores natus repellat necessitatibus, neque aperiam. Quos repellat explicabo, quaerat, ab rem laboriosam voluptatem asperiores, ullam veniam commodi harum! Autem, necessitatibus?
	Optio minus similique obcaecati doloremque corrupti pariatur! Corrupti in consequuntur inventore odit recusandae aperiam aspernatur, consequatur voluptates architecto officiis rem et laudantium impedit placeat dolorem expedita ipsa esse voluptatum neque!
	Illum quod perferendis eaque eius, amet voluptate totam consequatur veniam sint. Error quod praesentium eaque cupiditate ducimus incidunt, consectetur ullam aperiam optio perferendis, libero obcaecati tempore nisi facere, iure unde.
	Delectus animi repellendus excepturi dicta distinctio expedita est odio laudantium adipisci ullam blanditiis architecto, voluptates sint porro, laboriosam facilis obcaecati sunt explicabo numquam nulla aperiam? Saepe maiores consequuntur voluptates nam.
	Debitis voluptas placeat, voluptatum enim alias quae suscipit. Culpa inventore, illo atque rem labore deserunt officiis nobis, deleniti consequatur incidunt nam aperiam ipsam voluptatibus sed repudiandae recusandae quos hic est.
	Voluptatum exercitationem fuga excepturi nulla saepe, officiis accusantium pariatur reiciendis alias tenetur corporis illo assumenda omnis quae tempore quis molestiae eius sint est eligendi voluptate ex? Est sint sit facere.
	Voluptate debitis rem earum quibusdam nam impedit nesciunt et tempore magni, praesentium quos! At excepturi quo maiores corrupti iste accusamus ad, enim suscipit a rem vero numquam itaque cumque labore.
	Illo debitis alias sit sed ad, ipsum beatae provident et autem minima ex corporis adipisci ratione fugit dolore ab optio repellendus dolorum ipsa illum enim doloremque quidem modi! Dolores, quae.
	Maiores consequuntur labore itaque voluptas aut sed tempora eius cupiditate possimus vel, earum perspiciatis alias quis ipsam necessitatibus cum enim dolores molestiae aliquam ex dolorem repellendus dicta at. Pariatur, id!
	Eius nihil aut, adipisci nam ut in et optio ipsum, maiores natus a aliquam numquam sed quas qui distinctio odit! Itaque, quisquam perspiciatis. Quisquam totam voluptate consectetur, repellat recusandae temporibus.
	Harum officiis nihil in odit! Ex aliquam autem odit rem provident. Atque, non corporis dolorum odit aliquam nam necessitatibus architecto vitae repellendus, voluptate repudiandae a sapiente temporibus quidem laboriosam et!
	In eligendi voluptas perspiciatis delectus asperiores, necessitatibus iure distinctio rerum, quas totam illo. Ratione atque laboriosam hic blanditiis maiores, expedita omnis veritatis illo non numquam, tempore consequuntur dolorem soluta magnam.
	Dignissimos commodi illum eveniet quasi repellendus maiores unde tenetur saepe officia, rerum sapiente eum, tempora sequi quidem, laudantium consequatur labore. Dolores illo, ut a adipisci veritatis consequatur nam ducimus eum.
	Quasi debitis consequatur officia harum sit! Quasi animi in molestias, nulla exercitationem eveniet ab doloremque officiis suscipit ipsa aperiam accusantium reiciendis est vel odit illum ducimus? Tempora dolorum eius molestias.
	Cum temporibus quasi nostrum corrupti accusantium fugiat quod. Corporis consequuntur velit nulla sapiente modi explicabo ipsam itaque omnis odit, non dolores! Quia praesentium magnam quaerat molestias quo impedit? Voluptatibus, beatae!
	Minus voluptatem facere dolor soluta ipsam cumque unde pariatur consequuntur. Eveniet, soluta non! Facilis praesentium quisquam necessitatibus recusandae. Cum, impedit ut reprehenderit veritatis aut ullam asperiores nemo labore molestiae inventore?
	Deserunt ea autem quis repudiandae perspiciatis vitae modi doloribus sed officia voluptates optio quaerat assumenda accusamus hic ex id, maxime pariatur! Reiciendis, nam doloribus! Molestias autem aut porro maxime explicabo.
	Totam non, debitis, impedit itaque ad est temporibus blanditiis minima repellat aliquid nihil, ipsum dolore qui eius error inventore nemo aperiam! Quisquam repudiandae consequatur placeat cupiditate deserunt atque commodi omnis!
	Asperiores, iusto. Placeat sed animi delectus dolorum autem eius tempora et. Quasi eveniet quos labore officiis illum natus quisquam laudantium aperiam ab. Sunt ea eum facilis nulla quisquam? Id, suscipit?
	Ea quasi dicta nihil quo aperiam unde commodi modi doloremque autem mollitia, eligendi natus numquam odio facere ipsa repudiandae voluptatibus perferendis illo magnam eum illum a optio consectetur assumenda. Vitae.
	Fugiat sunt quod tenetur. Nam dignissimos suscipit eos magnam amet neque eius libero facilis sint aspernatur possimus nisi assumenda, voluptates necessitatibus quae iure sapiente et quibusdam ipsum placeat enim. Possimus.
	Molestiae est recusandae impedit debitis fugit, officiis facere quae quidem alias doloribus nesciunt. Illum aperiam, cupiditate, incidunt tempore quibusdam dignissimos itaque totam quod consectetur voluptatem beatae! Illum debitis alias expedita.
	Totam laborum, ratione facilis ex veritatis labore alias, vitae porro aliquam commodi ipsa esse doloremque aspernatur sapiente inventore illo ad minima voluptatum iure hic dicta consequuntur voluptates numquam possimus. Optio.
	Architecto doloribus deleniti omnis ea error eos mollitia quam eaque aliquid! Nobis, beatae et quam omnis vitae odit fugiat eaque magni quaerat culpa reprehenderit odio consequuntur. Suscipit fugiat quibusdam velit.
	Natus sed, aliquid iure dolorum tenetur ratione facere inventore dignissimos quasi nam cum cumque ex ducimus odio quod reiciendis rem? Debitis ullam sequi mollitia quisquam voluptas et saepe nobis laboriosam.
	Modi a repellat neque aliquam et ab dignissimos eaque nostrum recusandae vel dolor quam repudiandae, harum laudantium iusto nam aliquid explicabo ipsam quis. Debitis vel perspiciatis laborum asperiores pariatur magnam.
	Ex exercitationem officia sit quam a quae totam porro provident ad esse temporibus voluptatem maxime dolores eius necessitatibus aut tempore ut similique officiis, voluptas nostrum optio. Aspernatur tempora quidem qui.
	Hic totam vero commodi ipsa perspiciatis dignissimos necessitatibus, eaque laudantium atque placeat molestiae est nobis autem laborum cumque voluptatum doloribus. Voluptates, placeat. Aliquid corporis voluptas tenetur. Pariatur atque iste fugiat!
	Commodi fuga eos eaque facilis saepe, magni officiis cupiditate quibusdam voluptatibus necessitatibus fugiat fugit debitis pariatur, ab repudiandae totam aut accusantium soluta eum sint ipsum atque. Rerum eligendi perferendis provident.
	Magnam aliquam quaerat nostrum dolores omnis tempore doloremque officiis, velit perspiciatis quae facere rerum vero reprehenderit ad ratione molestiae modi. Ducimus asperiores, aut nulla nam aperiam nemo perspiciatis iste! Sint.
	Eveniet repudiandae praesentium sed doloremque et nemo quidem reiciendis ullam eos eaque voluptas doloribus impedit, beatae cumque esse eligendi vel iusto voluptates! Repellat dignissimos vero optio cupiditate odit dicta quae!
	Officiis quia eveniet, esse, laudantium ullam, nisi tenetur minus eius perspiciatis quisquam sapiente! Tenetur libero aliquid minima, quisquam soluta provident? A veniam iure explicabo optio eius, non labore quam aperiam!
	Accusamus, libero sint! Saepe, similique quasi. Tempore sunt illum modi possimus doloribus minima cum quasi quisquam. Aliquam corporis veniam blanditiis labore nihil, amet doloremque! Porro ex autem odit velit deserunt.
	Excepturi, ad officia ab nisi exercitationem et odio, ea vitae iste deleniti eligendi eaque, quidem perferendis a ut similique quibusdam magni placeat sed fuga id voluptas. Repellendus labore ipsum accusantium.
	Recusandae, omnis esse? Modi, voluptatum? Veniam, beatae! Ipsum quis incidunt vel, molestiae dignissimos numquam distinctio. Quam esse ducimus magni dolor eius neque harum maxime sequi architecto? Eaque blanditiis illo dolores!
	Voluptatum, officiis tempora ratione exercitationem ipsam dolorem similique facilis error doloribus reprehenderit quam, natus obcaecati eaque perspiciatis minus, fugit repellat consequuntur eum. Error, nam est. Laudantium sequi distinctio tenetur fuga?
	Debitis, velit quos iusto, quod libero sed sit dolores sapiente reiciendis, tempora atque. Cupiditate ducimus, totam ipsa minus, enim ex fuga tempore ad earum, reprehenderit sint facilis obcaecati vel. Ratione!
	Ex beatae maiores excepturi deleniti nesciunt debitis sed corrupti, aut distinctio similique eveniet a veritatis dignissimos esse eaque maxime asperiores blanditiis tenetur? Nisi rem, saepe consequatur repudiandae aperiam a dicta!
	In quo laboriosam, itaque quia nam deleniti officia mollitia explicabo vitae consequuntur natus laudantium quasi enim commodi, nulla quos aut qui veniam saepe atque nihil obcaecati quidem! Adipisci, reiciendis? Consectetur?
	Animi cupiditate officiis facilis numquam deleniti iusto commodi autem totam eos, illo eum similique saepe praesentium odit minus harum! Voluptates, qui quo. Magnam deserunt ea repellendus officiis, error eos quos.
	Earum, expedita libero suscipit doloribus, ducimus laudantium quod esse, possimus pariatur assumenda sed! Quaerat sequi, laudantium ducimus officiis iste accusantium beatae culpa iure assumenda, facere inventore reprehenderit eaque maiores libero?
	Illo reprehenderit cumque ab iure tempora ut nisi, sint neque dolores. Optio minus quaerat vero harum quam fugit asperiores ex molestiae eos, fugiat ipsum! Quaerat autem quam sit deleniti possimus.
	Velit atque ipsum amet quas deleniti perspiciatis nostrum minus dolores veritatis veniam vitae, laboriosam omnis a error, odit asperiores repellendus eaque sed animi sunt. Esse aperiam eaque pariatur minima unde.
	Ducimus dignissimos, tempora incidunt neque vel recusandae illo eligendi perspiciatis magnam veniam quae commodi qui, vitae odio ab. Temporibus delectus cum voluptate incidunt dolor, soluta ducimus id quod numquam nam!
	Perspiciatis, eveniet beatae. Molestias, placeat doloribus iusto ut, iure odio neque beatae perferendis adipisci assumenda pariatur voluptatem labore facilis reiciendis laboriosam officia? Quaerat, sunt expedita et qui tempore nesciunt adipisci?
	Tempore quam, repudiandae ipsa quidem doloribus ipsum magnam minima, atque earum fuga, et obcaecati sit illo deserunt labore dolorem eum sapiente ullam consequuntur. Rem earum maxime quia repudiandae provident veniam.
	Obcaecati quos maxime, laudantium deserunt eos voluptas adipisci ab labore reprehenderit ut repellat a dicta nam consectetur! Doloremque esse ad, molestias sequi, non quam, hic ab nobis incidunt necessitatibus quos?
	Accusantium inventore soluta maxime veniam laboriosam molestiae. Deserunt eum magnam, dolorem aperiam provident fuga aspernatur dolor voluptatibus quam velit corporis repellat iste. Mollitia quos id rerum alias dolorum repudiandae. Numquam?
	Voluptas vero placeat vel perspiciatis facere excepturi itaque? Eius iste tempora consequuntur harum dolores voluptate. Expedita, ipsam dignissimos! Temporibus similique corporis sunt sed dolor! Rem quas perferendis nesciunt tenetur error?
	Adipisci, harum in cum maiores consectetur expedita voluptatum, incidunt iste asperiores nemo tempora consequuntur doloribus recusandae reiciendis aliquid, quaerat eos praesentium odio nulla eaque laborum quis. Consequuntur sit laudantium tempora.
	Totam, esse laudantium ex quis quo corporis hic voluptates consectetur consequatur sit illo voluptas quasi labore dolor alias amet dolore placeat earum mollitia at. A quo sapiente eos sint rem.
	Odit, officiis deserunt? Nihil molestias quisquam nemo ad, dolor quam nulla! Molestias cumque alias provident quas sed minus sit quae aut iste eaque, officiis blanditiis architecto. Laborum, cumque. Iste, mollitia.
	Blanditiis dolores a doloremque qui perspiciatis omnis porro atque commodi doloribus sequi ipsam eos fugit accusamus, repellat, odio totam voluptatum nostrum dolorum eum nobis aperiam assumenda minus. Voluptas, dicta. Vel.
	Et ipsa placeat quaerat autem id cumque doloremque corporis explicabo rerum, saepe tenetur harum nobis modi sunt officiis ipsam doloribus iste consectetur, quidem architecto? Ullam ratione consequuntur neque quos dignissimos?
	Dicta ut, sed laudantium fuga totam maiores in repudiandae hic deleniti odio, quidem quisquam beatae illo quasi cumque eligendi ex qui ducimus? Veritatis voluptatem esse voluptatum ullam consequatur animi sunt!
	Ex, quidem consequuntur suscipit optio possimus, velit eveniet laudantium exercitationem omnis rerum iusto esse eum earum odit dolorum alias est neque consectetur accusamus veniam? Nam consequuntur omnis obcaecati possimus laboriosam?
	Doloribus incidunt, totam dolorem magni minima id ducimus quo tempore fuga laborum cum rem. Itaque suscipit necessitatibus neque, blanditiis cumque porro laborum iusto rerum. Omnis architecto praesentium adipisci qui optio.
	Hic illo placeat quae similique totam cupiditate harum iure voluptates rerum libero, asperiores aut, ab numquam illum impedit soluta nam dolores. Quod sed, possimus ad odit itaque iusto quia iure?
	Itaque consectetur eum voluptatibus molestias. Ipsum laboriosam obcaecati esse optio molestiae minus dignissimos, adipisci totam quaerat a vitae beatae saepe? Sunt quidem, impedit eos commodi exercitationem molestiae nisi delectus facilis.
	Porro optio consequatur dignissimos exercitationem impedit nihil veniam laborum odio quod ipsum, id, nemo blanditiis incidunt! Totam veritatis obcaecati esse omnis. Error sequi nesciunt voluptatum ipsum! Unde dolor asperiores quisquam?
	Nemo animi inventore voluptate veniam blanditiis reiciendis, rem voluptatem ex quam expedita iusto commodi a repudiandae magnam aut eos eligendi minima, quis ipsam exercitationem totam necessitatibus, sit dolore. Omnis, veniam?
	Corporis, neque optio. Iste, minima? Voluptas, dolore alias esse quae error expedita magni, molestias voluptates libero omnis in quis cum accusantium excepturi delectus animi voluptate, debitis repellendus similique! Dolorem, voluptatem.
	Rem, culpa obcaecati dolore nobis ipsa earum cupiditate, quisquam architecto provident unde quas placeat magni odio! Praesentium nemo iure magni unde, cum dignissimos consequuntur tempore, rerum explicabo tenetur vel sit!
	Labore quam et accusamus accusantium deleniti incidunt fugit maxime ad modi quasi eveniet, sequi eius aliquam porro earum? Reprehenderit facilis odio esse tempore dolores officia incidunt cupiditate rerum minima debitis.
	In ducimus temporibus et ratione iste, animi illum ad adipisci aperiam dolores nesciunt nisi ea molestiae modi. Quam, tenetur vitae enim id, eaque ipsam eum molestiae quos incidunt recusandae sunt.
	Minima ipsa dicta hic labore excepturi doloribus earum, ex quam voluptatibus rem possimus praesentium dolor natus nemo officia aperiam molestias adipisci reiciendis provident veniam? Deleniti, veritatis? Amet accusantium dicta nisi.
	Beatae fugiat amet labore magni commodi mollitia, eos eveniet exercitationem perferendis facilis rerum vero corrupti est vel vitae cum sunt dignissimos pariatur. Temporibus voluptatem aut quibusdam hic dolor sed voluptate.
	Maxime laudantium molestiae aperiam soluta nulla quam doloribus, dolorem facilis alias illo assumenda eaque voluptatibus tempore dolores rerum vel, vitae nostrum officia voluptatem cum. Exercitationem quaerat suscipit blanditiis sit sunt?
	Quis odio rerum sapiente, recusandae, maiores at quaerat voluptatibus, ut perspiciatis autem dignissimos quo facilis tempore eius? Consectetur possimus, fuga quia esse ad nostrum aperiam in. Natus unde aliquam consequuntur?
	Magnam fuga animi cum provident. Dolores reprehenderit voluptatum perferendis aperiam temporibus doloribus deserunt dolorum, natus voluptates dolorem similique. Excepturi atque corrupti, consequuntur officiis maxime et eos soluta nulla error. Nesciunt?
	Suscipit explicabo adipisci laboriosam aliquam aspernatur rem qui ullam provident vero. Aliquam velit minus, tempore doloremque iure aliquid recusandae harum voluptatibus obcaecati ratione placeat ipsa labore earum quas dolores veniam.
	Atque temporibus velit id ut modi ad qui iste, tempore eaque commodi natus reprehenderit eos perspiciatis adipisci earum eligendi quae, veritatis voluptatem expedita accusantium animi nostrum, libero cum! Vel, rerum?
	Sequi delectus, tempora recusandae aspernatur maiores possimus laudantium totam, officia atque, molestiae qui animi illum. Aut, vel ea nostrum quam facere aspernatur facilis beatae quod dignissimos laboriosam similique quas optio.
	Ipsam iusto hic at! Nobis iusto magnam, modi quaerat nesciunt quidem alias hic dolores corporis fuga dolorem veniam facilis laborum nam ipsum. Autem nemo non enim ad, nostrum aperiam quibusdam?
	Commodi quaerat laudantium illum officiis natus pariatur odit repellendus dicta maiores. Quas quam dolor atque debitis laboriosam aliquid! Eum nesciunt placeat fugiat, esse aliquam dolores vel voluptate earum cumque eaque.
	Repudiandae alias iusto eum tempora esse! Quibusdam accusamus aut consectetur, obcaecati magni dignissimos reprehenderit nam, autem aliquam ipsum saepe earum aperiam temporibus sint? Incidunt aliquid dignissimos reiciendis optio minima eligendi.
	Cum reiciendis vitae excepturi, aperiam molestiae eaque! Nisi cumque quae minus doloremque, impedit corporis voluptates praesentium asperiores vitae earum dolore ut commodi unde, dicta non eum. Quam nisi quibusdam repudiandae.
	Dolorum saepe inventore nemo, impedit error ab pariatur quo officia nihil fugit quaerat eius nostrum enim, temporibus earum sapiente labore aut aliquam eum vero. Atque tempore tenetur a impedit porro.
	Impedit nobis incidunt voluptas saepe sunt neque modi? Non necessitatibus odit fugit iusto impedit voluptatibus rerum aliquam, ipsa nam ducimus veritatis soluta praesentium! Illo qui quisquam possimus minus pariatur assumenda.
	Quam repellendus dolor, rem ratione error deleniti quos suscipit autem recusandae cupiditate quo, voluptas aspernatur sit incidunt molestiae eius obcaecati at sequi, voluptatibus omnis. Doloremque rerum commodi neque molestiae nobis?
	Inventore voluptas eos optio adipisci exercitationem molestias fugit. Animi accusantium illo voluptatibus provident omnis. Est itaque minima quasi, doloribus pariatur tenetur nostrum voluptatem. Consequuntur, necessitatibus vitae a dolorem dicta quo?
	Saepe omnis dolorum, sequi vero incidunt laborum. Distinctio assumenda culpa eaque, voluptatum deleniti cum, ipsum tempora ipsa quo quibusdam amet expedita quae cumque minima exercitationem eum perspiciatis voluptatibus tenetur quam!
	Molestias at repudiandae dicta ducimus delectus quam et doloremque commodi officia velit rerum in, praesentium accusamus cupiditate quis placeat ex est. Nesciunt ipsum quaerat quam, adipisci laboriosam velit sit aut?
	Alias, voluptates laborum velit expedita amet dolores inventore! Enim, dolor. Ullam fugiat velit minus facere laboriosam earum dolorum adipisci, pariatur, odio, molestiae culpa ratione dolores maiores? Ratione minus ab ea!
	Similique, molestias. Consequatur earum natus minima quo. Dignissimos eveniet ut consectetur sunt velit aspernatur vero iste quam minima provident. Fuga corrupti ut suscipit esse. Repellendus vitae expedita ut nemo iusto.
	Veritatis recusandae alias consectetur beatae nostrum optio velit qui quae, aut tempore tenetur maiores modi et dolores? Est, distinctio eum quibusdam quaerat eius ea. Architecto eaque commodi doloribus asperiores aut!
	Deserunt, voluptatum quasi commodi alias animi ex tempora perferendis consequuntur, culpa maxime, consectetur assumenda nisi neque dolorem dicta sunt nemo tempore soluta temporibus quaerat? Eaque eos necessitatibus inventore alias doloribus!
	Iusto animi perspiciatis, voluptatem et, quo corporis, dolorum reiciendis non ut magnam magni? Explicabo adipisci eveniet nihil alias voluptatum odio error quia similique? Maiores adipisci amet reprehenderit ratione odit voluptatum.
	A reprehenderit id eos, minus voluptatum quasi hic illum quod vero voluptates voluptate debitis autem ducimus maxime perspiciatis. Neque laborum saepe esse qui fuga sequi sint similique dolorum excepturi blanditiis.
	Libero fugit vitae et, minima esse molestiae facilis sit, laudantium tempora perferendis nobis, dolores numquam suscipit quas eius quos nihil ratione error quis quia possimus odit! Exercitationem provident error perferendis.
	Repellat autem explicabo saepe reprehenderit sit praesentium quaerat id quae, vitae omnis molestias unde rerum molestiae quibusdam provident, distinctio ipsam nisi reiciendis est perferendis sapiente? Saepe itaque iste minus facere?
	Mollitia voluptates magnam veniam nemo fuga labore non officiis perferendis qui? Labore, quia possimus? Molestias quos nihil excepturi ipsum? Vero facilis accusantium eos numquam molestias provident neque molestiae odio labore.
	Architecto quos eaque laboriosam tempora cupiditate tempore porro commodi accusantium voluptatum neque beatae, laborum voluptate. Officiis dolores similique ab. Iusto consequuntur corrupti ex iste quia ab adipisci vel ea quam.
	Soluta ratione et amet veniam maxime quis veritatis quibusdam. Enim labore sunt temporibus quis saepe, quo alias similique, corrupti illum dolorem distinctio aliquid? Corrupti repellat commodi, saepe nisi sint excepturi?
	Odio quidem dignissimos soluta nemo aut itaque, nam rem mollitia quo laudantium sunt reprehenderit consequuntur incidunt minima tempore perferendis explicabo nisi! Nostrum libero animi voluptatibus a porro possimus odit quos.
	Repudiandae quod, facere reprehenderit minus ipsa saepe? Dolores ut hic repudiandae ullam laborum corrupti quidem deleniti nulla! Repellat iste, aut vitae corrupti itaque dolores unde beatae atque veritatis quae nulla!
	Repellendus alias doloribus libero, ad non maxime deleniti aspernatur accusantium dignissimos similique asperiores distinctio nobis explicabo corporis fugiat ipsam voluptas officiis sunt sit. Omnis, eveniet maxime pariatur velit consectetur suscipit.
	Laudantium nemo quas cupiditate fugit vero, eius quis porro harum provident est mollitia aliquam distinctio soluta totam iusto modi numquam quidem temporibus illum dolorem. Autem, reiciendis. In harum totam esse.
	Iste qui nostrum officia minima hic cum natus, praesentium non temporibus, corrupti odit numquam laborum labore quidem veniam quod aspernatur, nemo adipisci ad molestiae deleniti? Id corrupti ducimus eligendi magni.
	Maiores, eos sapiente? Nemo facere pariatur eum numquam tempora soluta fuga natus perspiciatis, assumenda perferendis, aut illum! Modi quis obcaecati nisi esse repudiandae, amet temporibus inventore! Voluptatum dolorem quam enim.
	Dolor soluta debitis illum, quisquam vel numquam non odio modi beatae totam rerum? Ab, vel nesciunt, dicta cupiditate unde odit cumque excepturi provident iure inventore officia, magni neque temporibus et!
	Culpa perferendis nulla ipsum. Similique eaque obcaecati tempore quod perspiciatis facere, illo possimus accusamus in voluptates aspernatur temporibus odit dolores ab commodi excepturi natus harum facilis ex vero suscipit eos.
	Repudiandae modi, mollitia labore similique aperiam alias iure, obcaecati soluta, optio nobis eius. Sapiente molestiae quia deserunt quae impedit minus tempore non aliquid maxime placeat. Incidunt sint distinctio quasi necessitatibus?
	Reiciendis sunt exercitationem temporibus cum ducimus, illo rem earum, laudantium voluptas nostrum ratione culpa et quidem provident sequi soluta quia quas. Numquam perspiciatis, eveniet ad veritatis eaque porro. Quisquam, repellendus!
	Porro nihil deserunt atque velit eaque blanditiis harum nostrum praesentium minima reprehenderit consequuntur sit doloremque culpa quo quasi corporis dolores reiciendis quidem dolorum maiores saepe voluptas, ad ducimus. Ea, veritatis!
	Explicabo exercitationem delectus aliquid eligendi quibusdam, soluta necessitatibus excepturi unde ea, officiis provident nulla expedita magni ad nisi saepe in eum non, dolor sint corporis laudantium quae. Deleniti, dicta dolor.
	Cumque et pariatur explicabo suscipit, inventore labore accusantium similique vero possimus nulla quae, sed, illo dolores! Dolore voluptatem adipisci numquam suscipit in? Mollitia, obcaecati nihil quas dignissimos quidem rem enim.
	Fugit, eum dolorem impedit possimus nemo dolor deleniti perferendis minus consequuntur veritatis laboriosam voluptate dicta illo officiis illum enim modi dolorum omnis aperiam incidunt, ut ipsam! Omnis tenetur sit dignissimos.
	Voluptatum reiciendis porro labore in corporis blanditiis sit fugit, iste maxime enim dolorem assumenda esse reprehenderit, accusantium quia eum. Amet eos ex voluptas fugit magnam adipisci tempora sed accusantium? Eaque.
	Veniam similique, autem ab labore delectus quo velit adipisci amet, repudiandae facilis maxime itaque? Reiciendis reprehenderit enim qui, ab, magni aspernatur est numquam maiores rerum ut illo sunt esse officiis!
	Est distinctio praesentium, fugit saepe qui magni eos dolores ex eius nulla. Quae neque dolorem soluta illum deserunt voluptatem porro ut? Nisi eos consectetur, fuga eveniet voluptate suscipit magnam ipsa.
	Accusantium repellat dicta molestiae dolores nam facere iusto possimus molestias qui temporibus explicabo ducimus similique inventore, debitis a asperiores sapiente, quod aperiam veniam provident magnam. Odio porro perferendis incidunt deserunt.
	Magni doloremque, dolorem modi eaque expedita libero atque vel cum quos! Tempore molestias repellat sequi nam sunt numquam doloremque, ipsam odio. Assumenda porro molestias ea ab quod voluptates, officiis dolores.
	Rerum nesciunt qui incidunt, dolorem a eum! Obcaecati temporibus facere alias ratione laudantium corrupti dolore nulla architecto nostrum molestiae. Eaque id ipsum eum aut dolorem aperiam nobis! Facilis, delectus iure!
	Perspiciatis eos modi, reiciendis perferendis excepturi nulla harum, blanditiis dolorum dolorem laudantium omnis fuga incidunt iure consequuntur eius itaque voluptate debitis facere. Eum, voluptas pariatur. Accusamus placeat consequuntur nam enim!
	Doloribus harum dolorem, accusantium cupiditate perferendis, necessitatibus minima distinctio maiores facere rerum sint beatae corporis nemo eius. At sed obcaecati, nam pariatur ratione similique odit nesciunt voluptatibus beatae ex quo!
	Temporibus doloribus officia natus laudantium tempore commodi exercitationem assumenda quisquam! Cumque porro architecto, minus vero facere aperiam nihil rerum! Eligendi delectus consequatur laudantium cum, qui inventore nisi perspiciatis at deserunt.
	Incidunt, dolore ullam repudiandae facere ipsa mollitia quisquam voluptates eum recusandae sunt quia laboriosam iusto ut autem provident quod perspiciatis eaque, amet nihil quam aperiam voluptas esse voluptate? Suscipit, voluptatum!
	Est cumque, commodi illum officiis vero dolores reiciendis quas incidunt veniam quam eius quo et, expedita vel eum debitis porro minus hic aliquam adipisci. Sint quia debitis quidem hic ut.
	Ea accusantium quibusdam voluptate at nihil, ipsam praesentium mollitia soluta eveniet. Nostrum dolorem vitae saepe architecto sunt corrupti deserunt. Assumenda laborum distinctio quod eligendi exercitationem dicta nam tempore unde reiciendis.
	Saepe aperiam, deleniti error quo eius maiores dolor quidem eos eveniet ex quia sed veritatis reiciendis incidunt obcaecati alias dicta fuga aspernatur cupiditate quam laudantium. Unde aspernatur magnam nesciunt ipsum.
	Omnis sed magni nulla obcaecati sunt iste, voluptatem vero. Cum, quisquam unde neque quasi voluptatibus, maxime voluptate debitis sequi pariatur laudantium quod assumenda nam voluptatum perferendis veniam ducimus! Architecto, consequatur!
	Eos placeat saepe, doloremque libero perspiciatis facilis asperiores magnam. Eum excepturi in temporibus illo praesentium fugiat eos numquam dolorem enim. Ipsum exercitationem at aliquam. Neque veritatis nulla doloribus ex deleniti.
	Molestiae ab rem illo cum modi est facere similique quae, natus debitis impedit incidunt blanditiis quia tempore distinctio ipsam. Earum atque laboriosam numquam quasi, quaerat consectetur facilis eos officiis nemo.
	Exercitationem, cupiditate accusamus quibusdam accusantium quasi ipsa eum animi ullam officia molestiae earum! Dolores itaque cupiditate libero id harum veniam, quaerat vel veritatis nam nesciunt! Cum repellat quos earum fugiat.
	Similique quod accusantium, quidem magni consequuntur perspiciatis nobis rem rerum totam amet! Molestias aperiam, minus dolores, debitis eius quo laborum voluptatibus explicabo sapiente perspiciatis impedit. Aperiam veritatis voluptas atque reprehenderit.
	Totam culpa rerum a nobis enim aspernatur iusto numquam odit, repellat, et expedita adipisci minus vero placeat? Unde, molestias accusantium at error vitae eaque dolorum eum odio voluptate culpa dolor.
	Nemo ipsa consequatur praesentium rerum quibusdam aliquam quo, quasi aperiam suscipit corrupti veritatis repellendus amet hic. Suscipit deleniti rem temporibus officiis alias modi mollitia, esse dignissimos tenetur delectus tempore? Deleniti?
	Magni, dolorem praesentium ex excepturi quae, officiis aliquam distinctio necessitatibus minus animi in explicabo saepe earum, voluptate obcaecati beatae asperiores consequuntur maiores error eligendi voluptas omnis. Non dolor quaerat incidunt.
	Recusandae culpa ea ab amet quos id inventore? Officia earum accusamus voluptas eos, omnis numquam placeat? Enim quam velit impedit qui earum. Dignissimos sed excepturi iusto optio magnam maxime similique!
	Modi quas impedit, animi consequatur odit incidunt illum dicta delectus veritatis unde minima? Adipisci veritatis architecto odit quos natus exercitationem vel quis tempora eius eaque voluptates facilis, reprehenderit, id quibusdam.
	Eos explicabo minima aspernatur, quasi totam voluptas, perspiciatis necessitatibus similique quisquam enim temporibus possimus perferendis animi ea qui distinctio praesentium quos? At eligendi fugiat alias labore animi, asperiores nobis perferendis?
	Dolorum ab, nostrum consequatur ipsam in suscipit temporibus doloremque repellendus obcaecati nisi voluptatibus adipisci assumenda! Illo neque iure dolorem! Quam atque placeat aspernatur aliquam excepturi illo culpa iste sequi nemo?
	Accusamus doloremque in nihil minus? Culpa autem neque, eveniet perferendis illum voluptatum doloribus quia velit ex laudantium error unde iste eius deserunt. Illum doloremque quis itaque quasi? Similique, illo fugiat.
	Nihil repudiandae omnis necessitatibus maiores, voluptatem, quasi et quae adipisci quaerat quis ducimus iste corrupti esse. Laboriosam blanditiis ex quidem. Iste nulla hic excepturi, dolorem tempora maxime sint fuga. Eligendi.
	Autem eos nesciunt adipisci, a nobis sapiente! Perspiciatis aperiam, eius libero consectetur impedit repudiandae fuga beatae velit nihil magnam nobis. Quia veritatis iure aperiam porro vitae est hic id tenetur?
	Placeat nihil odit magnam hic nisi dolores beatae accusantium voluptatum deleniti doloremque, repudiandae sint voluptatem quia vel, provident et consequatur culpa labore optio corrupti non blanditiis. Modi animi autem similique.
	Incidunt ut voluptatum maiores facere quas itaque ratione libero, alias modi nisi autem vel similique. Facilis saepe minima aspernatur soluta, autem optio. Modi, nobis cumque. Id voluptas cumque sunt obcaecati.
	Aperiam, nisi quaerat eveniet consequatur, totam illum dolore at vel omnis consectetur error eaque quia placeat iure praesentium dolores. Iusto ut eos recusandae iure, libero consequuntur at sit maxime modi!
	Suscipit recusandae molestias eligendi, blanditiis est nobis ad commodi aperiam minima quaerat quas. Hic commodi, incidunt debitis impedit eum nihil praesentium quaerat suscipit ex consequuntur enim quasi eveniet cum velit.
	Sequi fugit asperiores quis. Esse explicabo nisi amet sequi vero aut aspernatur necessitatibus dolores culpa veritatis ea praesentium, magni eligendi excepturi hic delectus minima rem. Assumenda a dolore ipsa quam!
	Sint libero veniam eligendi possimus, at cupiditate architecto praesentium quidem, quis consequuntur, eveniet neque fugiat! Similique quidem voluptate quo voluptates possimus eligendi itaque! Nobis dicta vitae porro velit illum dolorem.
	Eligendi voluptatum odio rerum fugit magni molestias aspernatur, harum sunt nihil natus repudiandae. Reiciendis saepe, deleniti rem, eos doloribus quae repudiandae culpa voluptas autem voluptatibus nisi ex sunt et esse.
	Fugit ea voluptatem tempora nulla, expedita quam! Beatae eum necessitatibus, dicta doloribus sint at exercitationem quo, optio explicabo rerum quis iste mollitia odit placeat minima architecto sapiente nihil amet perspiciatis?
	Ut laudantium, numquam voluptates sequi deserunt soluta ipsa veritatis. Cupiditate quas corporis repudiandae dicta eos deserunt nemo sunt odio quasi harum, quos minima dolore sit autem aperiam dolorem consequuntur optio.
	Earum quaerat eius temporibus deleniti accusamus, nisi saepe autem qui perferendis explicabo iste maxime cum. Corrupti fugiat, assumenda veritatis aliquam quis quidem voluptas, dolores ipsa illum vero odit. Corporis, consectetur.
	Vero, commodi non? Unde, vitae. Laudantium impedit repellendus labore non error quasi fuga quam placeat voluptatem aut, ipsa, in iste ea nihil culpa. Voluptates in voluptatem consequatur odio officia fugiat?
	Quidem laudantium tempora ipsa rem dolores consectetur, tempore magnam non repellendus porro cupiditate odit quo exercitationem eum quae modi sapiente, in minus corporis unde iste. Recusandae similique esse magni ipsa.
	Alias unde nulla temporibus corporis voluptatibus, expedita ad quae provident quisquam perferendis inventore modi et, illum dignissimos blanditiis fugiat. Hic similique id, porro quibusdam tenetur quo debitis aliquam necessitatibus officia.
	Reprehenderit dolor eos placeat nesciunt alias dignissimos tempora esse minus, dolore, aspernatur fugit itaque quas error eaque. Perferendis, recusandae, est nostrum sed, nesciunt cumque ex illum at ad error harum.
	Odio, cum consectetur quibusdam iste quasi sint officiis quae quo, facilis velit repellendus ipsam? Enim, voluptatibus! Fugit reprehenderit iusto eaque ipsam unde nostrum enim sunt dolorem, ea cupiditate impedit necessitatibus!
	Totam aliquam praesentium, nihil, enim quia, alias eveniet quaerat harum sequi eligendi quos ea? Inventore sunt excepturi, quod, nobis eveniet dolores quos consectetur non eum eius repudiandae ex ducimus doloribus.</p>
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
