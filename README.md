Cirkeluppgift
=============
package 
{
	import flash.display.Sprite;
	import flash.events.Event;
	import flash.events.KeyboardEvent;
	import flash.events.MouseEvent;
	import flash.net.URLVariables;
	import flash.text.TextField;
	/**
	 * ...
	 * @author Adam Sjödahl
	 */
	public class Main extends Sprite 
	{
		
		private var sten:Vector.<Sprite> = new Vector.<Sprite>();
		private const nr_circles:int = 20;
		private var text:TextField;
		private var score:Number;
		private var bomb:Sprite = new Sprite();
		private var allCircles:Vector.<Sprite> = new Vector.<Sprite>
		public function Main():void 
		{
			if (stage) init();
			else addEventListener(Event.ADDED_TO_STAGE, init);
		}
		
		private function init(e:Event = null):void 
		{
			removeEventListener(Event.ADDED_TO_STAGE, init);
			// entry point
			
			text =  new TextField();
			text.x = 50;
			score = 0;
			stage.addChild(text);
			updateScore();
			
			for (var i:int = 0; i < nr_circles; i++)
			
		{  
			var cirkel:Sprite = new Sprite();
			cirkel.graphics.beginFill(0xff00cc);
		    cirkel.graphics.drawCircle(0, 0, 25);
			cirkel.graphics.endFill();
			addChild(cirkel);
			sten.push(cirkel);
			
			bomb.graphics.beginFill(0xff00cc);
		    bomb.graphics.drawCircle(0, 0, 25);
			bomb.graphics.endFill();
			addChild(bomb);
			
			bomb.y = Math.random () * stage.stageHeight - bomb.height;
			bomb.x = Math.random () * stage.stageWidth - bomb.width;
			bomb.addEventListener(MouseEvent.CLICK, bombClick);
			
			cirkel.y = Math.random () * stage.stageHeight - cirkel.height;
			cirkel.x = Math.random () * stage.stageWidth - cirkel.width;
			cirkel.addEventListener(MouseEvent.CLICK, bax)
			stage.addEventListener(KeyboardEvent.KEY_DOWN, resetStage);
			
		   }
		}   
	    private function makeCircles():void 
		{
			for (var i:int = 0; i < nr_circles; i++)
		
			{  
			var cirkel:Sprite = new Sprite();
			cirkel.graphics.beginFill(0xff00cc);
		    cirkel.graphics.drawCircle(0, 0, 25);
			cirkel.graphics.endFill();
			addChild(cirkel);
			cirkel.y = Math.random () * stage.stageHeight - cirkel.height;
			cirkel.x = Math.random () * stage.stageWidth - cirkel.width;
			cirkel.addEventListener(MouseEvent.CLICK, bax)
			allCircles.push(cirkel);
			}
		}
			
		
		
		private function resetStage(e:KeyboardEvent):void 
		{
			if (e.keyCode == 32)
			
			while (allCircles.length > 0) 
			{
				removeChild(allCircles[0]);
			    allCircles.shift ();
			}
			
			
			
			
			makeCircles ();
			
			score = 0;
			text.text = "Score: 0";
		}
		
		private function bombClick(e:MouseEvent):void 
		{
			for (var i:int = 0; i < nr_circles; i++)
			{
				sten[i].x = 8000;
				bomb.visible = false;
			}
		}
		
		private function bax(e:Event):void 
		{
			Sprite(e.target).visible = false;
			score++;
			updateScore();
		}
		private function updateScore():void 
		{
			text.text = "Score: " + score;
		}
		
	}
	
